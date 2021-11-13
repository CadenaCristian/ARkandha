# ARkandha

1. Creación de base de datos (Ejecute los script en orden )
----------------------(Primer script)----------------------------------
-- Database: plots_owners

-- DROP DATABASE plots_owners;

CREATE DATABASE plots_owners
    WITH 
    OWNER = postgres
    ENCODING = 'UTF8'
    LC_COLLATE = 'Spanish_Colombia.1252'
    LC_CTYPE = 'Spanish_Colombia.1252'
    TABLESPACE = pg_default
    CONNECTION LIMIT = -1;
----------------------(Segundo script)-----------------------------------
-- Table: public.owner_type

-- DROP TABLE public.owner_type;

CREATE TABLE IF NOT EXISTS public.owner_type
(
    id integer NOT NULL DEFAULT nextval('owner_type_id_seq'::regclass),
    name character varying(100) COLLATE pg_catalog."default" NOT NULL,
    CONSTRAINT owner_type_pkey PRIMARY KEY (id)
)

TABLESPACE pg_default;

ALTER TABLE public.owner_type
    OWNER to postgres;
----------------------(Tercer script)-----------------------------------
-- Table: public.owner_plost

-- DROP TABLE public.owner_plost;

CREATE TABLE IF NOT EXISTS public.owner_plost
(
    id integer NOT NULL DEFAULT nextval('owner_plost_id_seq'::regclass),
    catastral_id character varying(50) COLLATE pg_catalog."default" NOT NULL,
    plost_type integer,
    addres_name character varying(50) COLLATE pg_catalog."default" NOT NULL,
    realtor_name character varying(50) COLLATE pg_catalog."default" NOT NULL,
    owner_data integer,
    CONSTRAINT owner_plost_pkey PRIMARY KEY (id),
    CONSTRAINT fk_owner FOREIGN KEY (owner_data)
        REFERENCES public.owners (id) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION,
    CONSTRAINT fk_plost_type FOREIGN KEY (plost_type)
        REFERENCES public.plost_type (id) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION
)

TABLESPACE pg_default;

ALTER TABLE public.owner_plost
    OWNER to postgres;
----------------------(Cuarto script)-----------------------------------
-- Table: public.plost_type

-- DROP TABLE public.plost_type;

CREATE TABLE IF NOT EXISTS public.plost_type
(
    id integer NOT NULL DEFAULT nextval('plost_type_id_seq'::regclass),
    name character varying(100) COLLATE pg_catalog."default" NOT NULL,
    CONSTRAINT plost_type_pkey PRIMARY KEY (id)
)

TABLESPACE pg_default;

ALTER TABLE public.plost_type
    OWNER to postgres;

----------------------(Quinto script)-----------------------------------
-- Table: public.owners

-- DROP TABLE public.owners;

CREATE TABLE IF NOT EXISTS public.owners
(
    id integer NOT NULL DEFAULT nextval('owners_id_seq'::regclass),
    type_owner integer,
    identification character varying(100) COLLATE pg_catalog."default" NOT NULL,
    name_owner character varying(100) COLLATE pg_catalog."default" NOT NULL,
    CONSTRAINT owners_pkey PRIMARY KEY (id),
    CONSTRAINT fk_owner_type FOREIGN KEY (type_owner)
        REFERENCES public.owner_type (id) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION
)

TABLESPACE pg_default;

ALTER TABLE public.owners
    OWNER to postgres;
    
2. Creación del entorno virtual (Para este paso debe de tener la libreria 'pip' y debe de tener una version de python superior a las 3)
(comando #1) python3 -m venv entornoVirtual
(comando #2) cd entornoVirtual/Scripts
(comando #3) source activate
(comando #4) cd ..
(comando #5) cd ..
3. Clonar el repositorio Backend(Ejecute los comandos en el siguiente orden)
(Comando #6) git clone https://github.com/CadenaCristian/ARkandhaBackend.git
(comando #7) cd plots_owners_back/
(comando #8) pip install -r libs.txt
(comando #9) python manage.py runserver


4. Clonar el repositorio Frontend
(comando #9) git clone https://github.com/CadenaCristian/ARkandhaFrontend.git
(comando #10) cd plots_owners_front
(comando #11) npm i
(comando #12) npm run start
