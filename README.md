# ARkandha

1. Creación de base de datos (Ejecute los script en orden )<br>
----------------------(Primer script)----------------------------------<br>
-- Database: plots_owners<br>

-- DROP DATABASE plots_owners;<br>

CREATE DATABASE plots_owners<br>
    WITH <br>
    OWNER = postgres<br>
    ENCODING = 'UTF8'<br>
    LC_COLLATE = 'Spanish_Colombia.1252'<br>
    LC_CTYPE = 'Spanish_Colombia.1252'<br>
    TABLESPACE = pg_default<br>
    CONNECTION LIMIT = -1;<br>
----------------------(Segundo script)-----------------------------------<br>
-- Table: public.owner_type<br>

-- DROP TABLE public.owner_type;<br>

CREATE TABLE IF NOT EXISTS public.owner_type<br>
(<br>
    id integer NOT NULL DEFAULT nextval('owner_type_id_seq'::regclass),<br>
    name character varying(100) COLLATE pg_catalog."default" NOT NULL,<br>
    CONSTRAINT owner_type_pkey PRIMARY KEY (id)<br>
)<br>

TABLESPACE pg_default;<br>

ALTER TABLE public.owner_type<br>
    OWNER to postgres;<br>
----------------------(Tercer script)-----------------------------------<br>
-- Table: public.owner_plost<br>

-- DROP TABLE public.owner_plost;<br>

CREATE TABLE IF NOT EXISTS public.owner_plost<br>
(<br>
    id integer NOT NULL DEFAULT nextval('owner_plost_id_seq'::regclass),<br>
    catastral_id character varying(50) COLLATE pg_catalog."default" NOT NULL,<br>
    plost_type integer,<br>
    addres_name character varying(50) COLLATE pg_catalog."default" NOT NULL,<br>
    realtor_name character varying(50) COLLATE pg_catalog."default" NOT NULL,<br>
    owner_data integer,<br>
    CONSTRAINT owner_plost_pkey PRIMARY KEY (id),<br>
    CONSTRAINT fk_owner FOREIGN KEY (owner_data)<br>
        REFERENCES public.owners (id) MATCH SIMPLE<br>
        ON UPDATE NO ACTION<br>
        ON DELETE NO ACTION,<br>
    CONSTRAINT fk_plost_type FOREIGN KEY (plost_type)<br>
        REFERENCES public.plost_type (id) MATCH SIMPLE<br>
        ON UPDATE NO ACTION<br>
        ON DELETE NO ACTION<br>
)<br>

TABLESPACE pg_default;<br>

ALTER TABLE public.owner_plost<br>
    OWNER to postgres;<br>
----------------------(Cuarto script)-----------------------------------<br>
-- Table: public.plost_type<br>

-- DROP TABLE public.plost_type;<br>

CREATE TABLE IF NOT EXISTS public.plost_type<br>
(<br>
    id integer NOT NULL DEFAULT nextval('plost_type_id_seq'::regclass),<br>
    name character varying(100) COLLATE pg_catalog."default" NOT NULL,<br>
    CONSTRAINT plost_type_pkey PRIMARY KEY (id)<br>
)<br>

TABLESPACE pg_default;<br>

ALTER TABLE public.plost_type<br>
    OWNER to postgres;<br>

----------------------(Quinto script)-----------------------------------<br>
-- Table: public.owners<br>

-- DROP TABLE public.owners;<br>

CREATE TABLE IF NOT EXISTS public.owners<br>
(<br>
    id integer NOT NULL DEFAULT nextval('owners_id_seq'::regclass),<br>
    type_owner integer,<br>
    identification character varying(100) COLLATE pg_catalog."default" NOT NULL,<br>
    name_owner character varying(100) COLLATE pg_catalog."default" NOT NULL,<br>
    CONSTRAINT owners_pkey PRIMARY KEY (id),<br>
    CONSTRAINT fk_owner_type FOREIGN KEY (type_owner)<br>
        REFERENCES public.owner_type (id) MATCH SIMPLE<br>
        ON UPDATE NO ACTION<br>
        ON DELETE NO ACTION<br>
)<br>

TABLESPACE pg_default;<br>

ALTER TABLE public.owners<br>
    OWNER to postgres;<br>
    
2. Creación del entorno virtual (Para este paso debe de tener la libreria 'pip' y debe de tener una version de python superior a las 3)<br>
(comando #1) python3 -m venv entornoVirtual<br>
(comando #2) cd entornoVirtual/Scripts<br>
(comando #3) source activate<br>
(comando #4) cd ..<br>
(comando #5) cd ..<br>
3. Clonar el repositorio Backend(Ejecute los comandos en el siguiente orden)<br>
(Comando #6) git clone https://github.com/CadenaCristian/ARkandhaBackend.git<br>
(comando #7) cd plots_owners_back/<br>
(comando #8) pip install -r libs.txt<br>
(comando #9) python manage.py runserver<br>


4. Clonar el repositorio Frontend<br>
(comando #9) git clone https://github.com/CadenaCristian/ARkandhaFrontend.git<br>
(comando #10) cd plots_owners_front<br>
(comando #11) npm i<br>
(comando #12) npm run start<br>
