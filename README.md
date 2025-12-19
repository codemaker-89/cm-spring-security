CM SPRING SECURITY
------------------
A reusable Spring Boot security library that provides a ready-made implementation of JWT-based authentication, OAuth2 client integration, and common security APIs (login, logout, refresh token) so that consuming projects can skip writing repetitive security code.
This project is designed to be added as a dependency to other Spring Boot applications and plugged into their security configuration with minimal setup.

✨ Key Features
----------------
`````
   JWT token generation, validation, and refresh
   Standard authentication APIs (Login, Logout, Refresh Token)
   Custom JwtAuthenticationFilter
   Centralized Spring Security configuration
   Easy-to-use as a library dependency
`````
📦 Dependencies Used
---------------------
The project is built using the following core dependencies:

1. SPRING SECURITY & OAUTH
````` 
	a. spring-boot-starter-security – Core Spring Security framework
	b. spring-boot-starter-oauth2-client – OAuth2 login and client support
`````
2. JWT (JSON Web Tokens)
`````   
    a. jjwt-api, jjwt-impl, jjwt-jackson – JWT creation, parsing, and signing
    b. jjwt (0.12.5) – Latest JWT utilities
`````
🧩 Project Modules Overview
---------------------------
1️⃣ Authentication Module

  1. Responsible for:
`````
	User authentication
	JWT token generation
	Refresh token handling
`````
  2. APIs Provided:
`````
	POST /oauth/login
	GET /oauth/logout
	PUT /oauth/refresh
	This allows consuming applications to reuse authentication logic without re-implementing it.
`````
2️⃣ JWT Module

  1. Handles:
`````
   a.JWT creation and signing
   b.Token validation
   c.Claim extraction 
   d.Token expiration checks
`````
  2. Key Components:
`````
   a. IJWTService  
   b. JwtTokenUtil
`````
  3. Secret key & expiration configuration

3️⃣ OAuth2 Module

  1. Provides:
`````
   a. OAuth2 client configuration
   b. Token exchange handling
   c. Integration with Spring Security OAuth2 flow
`````
This allows applications to enable OAuth login without writing boilerplate code.

🔌 How to Use as a Library
---------------------------
Step 1: Add Dependency 

For Maven project
```
<dependency>
    <groupId>io.github.codemaker-89</groupId>
    <artifactId>cm-spring-security</artifactId>
    <version>RELEASE</version>
</dependency>
```
For Gradle Project 
```
implementation("io.github.codemaker-89:cm-spring-security:RELEASE")
````
Step 2: Scan all components of library and your project.

Use the following code in your main class. (Replace the default @SpringBootApplication annotation)
```
@SpringBootApplication(scanBasePackages = {"<your.project.package>","com.cm.security"})
````

⚙️ Application Properties Configuration
----------------------------------------
The library is configurable via application.yml or application.properties in the consuming application.

YAML Code
 ````
# ===============================
# Server Configuration
# ===============================
server:
  port: <your-port-no>
  servlet:
    context-path: /<your_app_context_path_name>

# ===============================
# Spring Application Name
# ===============================
spring:
  application:
    name: <your_application_name>
# ===============================
# Datasource Configuration
# ===============================
  datasource:
    driver-class-name: <database-driver-class-name>
    url: <database-url>
    username: <database-username>
    password: <database-password>
# ===============================
# JPA / Hibernate Configuration
# ===============================
  jpa:
    hibernate:
      naming:
        physical-strategy: org.hibernate.boot.model.naming.PhysicalNamingStrategyStandardImpl
    show-sql: true
    properties:
      hibernate:
        dialect: <database-dialect>
# ===============================
# Spring Configuration
# ===============================
  main:
    allow-bean-definition-overriding: true
    allow-circular-references: true
# ===============================
# Web / Error Configuration 
# ===============================						
  web:
    error:
      whitelabel:
        enabled: false

# ================================
# Custom CM Security Configuration
# ================================
#provide custom header for Context-Token and path that dont need token 
cm:
  security:
    custom-header: <your-custom-request-header>
    token-validity: 3600
    allowed-path:
    - /oauth/**
    - /actuator/**
````
Properties Code
`````
# ===============================
# Server Configuration
# ===============================
server.port=<your-port-no>
server.servlet.context-path=/<your_app_context_path_name>

# ===============================
# Spring Application Name
# ===============================
spring.application.name=<your_application_name>

# ===============================
# Datasource Configuration
# ===============================
spring.datasource.driver-class-name=<database-driver-class-name>
spring.datasource.url=<database-url>
spring.datasource.username=<database-username>
spring.datasource.password=<database-password>

# ===============================
# JPA / Hibernate Configuration
# ===============================
spring.jpa.hibernate.naming.physical-strategy=org.hibernate.boot.model.naming.PhysicalNamingStrategyStandardImpl
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=<database-dialect>

# ===============================
# Spring Configuration
# ===============================
spring.main.allow-bean-definition-overriding=true
spring.main.allow-circular-references=true

# ===============================
# Web / Error Configuration
# ===============================
spring.web.error.whitelabel.enabled=false

# ===============================
# Custom CM Security Configuration
# ===============================
cm.security.custom-header=<your-custom-request-header>
cm.security.token-validity=3600
cm.security.allowed-path[0]=/oauth/**
cm.security.allowed-path[1]=/actuator/**
`````

🌐 SETUP CORS CONFIGURATION
----------------------------
The Cross-Origin Resource Sharing is configurable via application.yml or application.properties in the consuming application.

YAML Code
````
cm:
    allowed-path:
    - /oauth/**
    - /actuator/**
    - /test/**
    enable-cors: true
    allow-credentials: false
    allowed-origins:
    - '*' # Allow from every origin
#   - http://localhost:3000
#   - http://localhost:3001
    allowed-methods:
    - POST
    - GET
    - PUT
    - DELETE
    - PATCH
    - OPTIONS
    allowed-headers:
    - Authorization
    - Accept
    - X-Context-Token
    - Content-Type
    - Access-Control-Request-Method
    - Access-Control-Request-Headers
    exposed-headers:
    - Access-Control-Allow-Origin
    - Access-Control-Allow-Credentials

````
Properties Code
`````
# ===============================
# CM Security / CORS Configuration
# ===============================

cm.allowed-path[0]=/oauth/**
cm.allowed-path[1]=/actuator/**
cm.allowed-path[2]=/test/**

cm.enable-cors=true
cm.allow-credentials=false

cm.allowed-origins[0]=*

# cm.allowed-origins[1]=http://localhost:3000
# cm.allowed-origins[2]=http://localhost:3001

cm.allowed-methods[0]=POST
cm.allowed-methods[1]=GET
cm.allowed-methods[2]=PUT
cm.allowed-methods[3]=DELETE
cm.allowed-methods[4]=PATCH
cm.allowed-methods[5]=OPTIONS

cm.allowed-headers[0]=Authorization
cm.allowed-headers[1]=Accept
cm.allowed-headers[2]=X-Context-Token
cm.allowed-headers[3]=Content-Type
cm.allowed-headers[4]=Access-Control-Request-Method
cm.allowed-headers[5]=Access-Control-Request-Headers

cm.exposed-headers[0]=Access-Control-Allow-Origin
cm.exposed-headers[1]=Access-Control-Allow-Credentials
`````
🗄️ SETUP DATABASE
------------------------------------------------
Set up a database using the following script in your preferred database system. The following script is for a PostgreSQL DB. 

SUBSCRIPTION-STATUS
`````
CREATE TABLE IF NOT EXISTS public.subscription_status
(
    id integer NOT NULL GENERATED ALWAYS AS IDENTITY ( INCREMENT 1 START 1 MINVALUE 1 MAXVALUE 2147483647 CACHE 1 ),
    status_name VARCHAR(50) COLLATE pg_catalog."default" NOT NULL,
    status_code VARCHAR(50) COLLATE pg_catalog."default" NOT NULL,
    description VARCHAR(100) COLLATE pg_catalog."default" NOT NULL,
    active BOOLEAN DEFAULT true,
    features JSONB DEFAULT '{}',
    entered_by character varying(50) COLLATE pg_catalog."default",
    entered_dt timestamp without time zone DEFAULT now(),
    updated_by character varying(50) COLLATE pg_catalog."default",
    updated_dt timestamp without time zone,
    CONSTRAINT subscription_status_pkey PRIMARY KEY (id),
    CONSTRAINT unq_sub_status UNIQUE (status_name),
    CONSTRAINT unq_sub_code UNIQUE (status_code)
    
)

TABLESPACE pg_default;

ALTER TABLE IF EXISTS public.subscription_status
 OWNER to postgres;

INSERT INTO public.subscription_status
( status_name,status_code,description,active,  entered_by)
VALUES('Trial','T','Trial Status', true, 'system');

INSERT INTO public.subscription_status
( status_name,status_code,description,active,  entered_by)
VALUES('Active','A','Trial Status', true, 'system');

INSERT INTO public.subscription_status
( status_name,status_code,description,active,  entered_by)
VALUES('Suspended','S','Trial Status', true, 'system');

INSERT INTO public.subscription_status
( status_name,status_code,description,active,  entered_by)
VALUES('Cancelled','C','Trial Status', true, 'system');

`````

SUBSCRIPTION-PLAN
`````
CREATE TABLE IF NOT EXISTS public.subscription_plans
(
    id integer NOT NULL GENERATED ALWAYS AS IDENTITY ( INCREMENT 1 START 1 MINVALUE 1 MAXVALUE 2147483647 CACHE 1 ),
    plan_name VARCHAR(50) COLLATE pg_catalog."default" NOT NULL,
    code VARCHAR(50) COLLATE pg_catalog."default" NOT NULL,
    description VARCHAR(100) COLLATE pg_catalog."default" NOT NULL,
    max_employees INTEGER NOT NULL,
    max_offices INTEGER NOT NULL,
    price_monthly DECIMAL(10,2) NOT NULL,
    price_yearly DECIMAL(10,2) NOT NULL,
    active BOOLEAN DEFAULT true,
    features JSONB DEFAULT '{}',
    entered_by character varying(50) COLLATE pg_catalog."default",
    entered_dt timestamp without time zone DEFAULT now(),
    updated_by character varying(50) COLLATE pg_catalog."default",
    updated_dt timestamp without time zone,
    CONSTRAINT subscription_plans_pkey PRIMARY KEY (id),
    CONSTRAINT unq_plan UNIQUE (plan_name),
    CONSTRAINT unq_code UNIQUE (code)
    
)

TABLESPACE pg_default;

ALTER TABLE IF EXISTS public.subscription_plans
 OWNER to postgres; 

INSERT INTO public.subscription_plans(plan_name,code,description,max_employees,max_offices,price_monthly,price_yearly,features,entered_by)
VALUES('Basic Plan','BASIC','Entry-level plan for small teams',10,1,499.00,4999.00,'{}','system'),
	  ('Standard Plan','STANDARD','Mid-tier plan for growing companies',50,5,1499.00,14999.00, '{}','system'),
      ('Premium Plan','PREMIUM','Advanced plan with full features',200, 20,2999.00,29999.00,'{}','system');

`````

TENANT
`````
CREATE TABLE IF NOT EXISTS public.tenant_master
(
    id integer NOT NULL GENERATED ALWAYS AS IDENTITY ( INCREMENT 1 START 1 MINVALUE 1 MAXVALUE 2147483647 CACHE 1 ),
    tenant_name character varying(50) COLLATE pg_catalog."default" NOT NULL,
    subdomain VARCHAR(100) UNIQUE NOT NULL,
    subscription_status INTEGER NOT NULL REFERENCES public.subscription_status(id),
    subscription_plan INTEGER NOT NULL REFERENCES public.subscription_plans(id),
    subscription_start_date DATE NOT NULL,
    subscription_end_date DATE,
    max_employees INTEGER NOT NULL DEFAULT 50,
    max_offices INTEGER NOT NULL DEFAULT 5,
    timezone VARCHAR(50) DEFAULT 'UTC',
    currency VARCHAR(3) DEFAULT 'USD',
    logo_url character varying(100) COLLATE pg_catalog."default" NOT NULL,
    primary_contact_email VARCHAR(255) NOT NULL,
    primary_contact_phone VARCHAR(20),
    active boolean DEFAULT true,
    settings JSONB DEFAULT '{}',
    entered_by character varying(50) COLLATE pg_catalog."default",
    entered_dt timestamp without time zone DEFAULT now(),
    updated_by character varying(50) COLLATE pg_catalog."default",
    updated_dt timestamp without time zone,
    CONSTRAINT tenant_master_pkey PRIMARY KEY (id),
	CONSTRAINT unq_tenant_master UNIQUE (tenant_name),
	CONSTRAINT unq_tenant_subdomain UNIQUE (subdomain),
	CONSTRAINT unq_tenant_email UNIQUE (primary_contact_email),
	CONSTRAINT unq_tenant_phone UNIQUE (primary_contact_phone)
);	

ALTER TABLE IF EXISTS public.tenant_master
 OWNER to postgres;
 
 INSERT INTO public.tenant_master
( tenant_name,subdomain,subscription_status, subscription_plan, subscription_start_date, subscription_end_date, max_employees, max_offices, timezone,
    currency,logo_url, primary_contact_email,primary_contact_phone,active, settings, entered_by
)
VALUES
(
    'Tenant Name', 'domain-name',1, 1, CURRENT_DATE, CURRENT_DATE + INTERVAL '1 year',100,10,'Asia/Kolkata','INR','https://example.com/logo.png',
    'admin@acme.com', '+91-9876543210', true,'{}','system'
);

`````	

ROLE-MASTER
`````	
CREATE TABLE IF NOT EXISTS public.role_master
(
    id integer NOT NULL GENERATED ALWAYS AS IDENTITY ( INCREMENT 1 START 1 MINVALUE 1 MAXVALUE 2147483647 CACHE 1 ),
    role_name character varying(50) COLLATE pg_catalog."default" NOT NULL,
    description character varying(100) COLLATE pg_catalog."default",
    active boolean DEFAULT true,
    tenant INTEGER NOT NULL REFERENCES public.tenant_master(id),
    entered_by character varying(50) COLLATE pg_catalog."default",
    entered_dt timestamp without time zone DEFAULT now(),
    updated_by character varying(50) COLLATE pg_catalog."default",
    updated_dt timestamp without time zone,
    CONSTRAINT role_master_pkey PRIMARY KEY (id),
    CONSTRAINT unq_role_master UNIQUE (role_name, tenant)
)

TABLESPACE pg_default;

ALTER TABLE IF EXISTS public.role_master
    OWNER to postgres;
    
INSERT INTO public.role_master(
	 role_name, description, active, tenant, entered_by)
	VALUES ( 'Platform Admin', 'Platform Administrator Role', true, 1, 'system');    
	
    
INSERT INTO public.role_master(
	 role_name, description, active, tenant, entered_by)
	VALUES ( 'Tenant Admin', 'Tenant Administrator Role', true, 1, 'system');  	

`````

USER-MASTER
`````
CREATE TABLE IF NOT EXISTS public.user_master
(
    id integer NOT NULL GENERATED ALWAYS AS IDENTITY ( INCREMENT 1 START 1 MINVALUE 1 MAXVALUE 2147483647 CACHE 1 ),
    full_name character varying(100) COLLATE pg_catalog."default" NOT NULL,
    email character varying(100) COLLATE pg_catalog."default",
    mobile character varying(12) COLLATE pg_catalog."default",
    staff_id character varying(15) COLLATE pg_catalog."default" NOT NULL,
    role_id INTEGER NOT NULL REFERENCES public.role_master(id),
    username character varying(50) COLLATE pg_catalog."default" NOT NULL,
    password character varying(100) COLLATE pg_catalog."default" NOT NULL,
    two_stage_enabled boolean DEFAULT false,
    password_reset boolean DEFAULT false,
    account_non_expired boolean DEFAULT true,
    account_non_locked boolean DEFAULT true,
    credentials_non_expired boolean DEFAULT true,
    active boolean DEFAULT true,
    tenant INTEGER NOT NULL REFERENCES public.tenant_master(id),
    entered_by character varying(50) COLLATE pg_catalog."default",
    entered_dt timestamp without time zone DEFAULT now(),
    updated_by character varying(50) COLLATE pg_catalog."default",
    updated_dt timestamp without time zone,
    CONSTRAINT user_master_pkey PRIMARY KEY (id),
    CONSTRAINT unq_user_master UNIQUE (username),
    CONSTRAINT unq_staff_id UNIQUE (staff_id, tenant),
    CONSTRAINT unq_email UNIQUE (email, tenant),
    CONSTRAINT unq_mobile UNIQUE (mobile, tenant) 
)

TABLESPACE pg_default;

ALTER TABLE IF EXISTS public.user_master
 OWNER to postgres;
 
 
 INSERT INTO public.user_master(
	full_name, email, mobile, staff_id, role_id, username, password, tenant, entered_by)
	VALUES ('Administrator', 'jayasankar.47@gmail.com', '9567675677', 'EMP-0001',1, 'admin', '$2a$10$euD7x8Iid6V2LpGKit6Ys.jiQ4LtTrpeYQejx9GQvjEGQYThcPLK.',1,'system'); 	

`````
	
JWT-TOKEN
`````
CREATE TABLE IF NOT EXISTS public.jwt_token
(
    id integer NOT NULL GENERATED ALWAYS AS IDENTITY ( INCREMENT 1 START 1 MINVALUE 1 MAXVALUE 2147483647 CACHE 1 ),
    access_token character varying(5000) COLLATE pg_catalog."default",
    refresh_token character varying(5000) COLLATE pg_catalog."default",
    username character varying(50) COLLATE pg_catalog."default",
    tenant INTEGER NOT NULL REFERENCES public.tenant_master(id),
    issued_at timestamp without time zone,
    expires_at timestamp without time zone,
    refresh_expires_at timestamp without time zone,
    active boolean,
    CONSTRAINT jwt_token_pkey PRIMARY KEY (id)
)


`````

CREDENTIALS
`````
CREATE TABLE IF NOT EXISTS public.credentials
(
    id integer NOT NULL GENERATED ALWAYS AS IDENTITY ( INCREMENT 1 START 1 MINVALUE 1 MAXVALUE 2147483647 CACHE 1 ),
    cred_name character varying(100) COLLATE pg_catalog."default" NOT NULL,
    cred_value character varying(100) COLLATE pg_catalog."default",
    active boolean DEFAULT true,
    entered_by character varying(50) COLLATE pg_catalog."default",
    entered_dt timestamp without time zone DEFAULT now(),
    updated_by character varying(50) COLLATE pg_catalog."default",
    updated_dt timestamp without time zone,
    CONSTRAINT credentials_pkey PRIMARY KEY (id),
    CONSTRAINT unq_cred UNIQUE (cred_name)

);

INSERT INTO public.credentials(cred_name, cred_value,  entered_by)
	VALUES ('aes-key', '6674fe3c340b10c3af52410670a1973e','system');	

`````
