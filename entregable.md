Table Users {
  user_id SERIAL Pk 
  name VARCHAR(100)
  email VARCHAR(100)  
  password VARCHAR(255)
  age INT
}

Table Roles {
  role_id SERIAL PK
  name VARCHAR(50)
}

Table UserRole {
  user_id INT
  role_id INT
  PRIMARY KEY (user_id, role_id)
}

Table Categories {
  category_id SERIAL PK
  name VARCHAR(100)
}

Table Courses {
  course_id SERIAL PK
  title VARCHAR(255)
  description TEXT
  level VARCHAR(50)
  teacher_id INT
}

Table CourseVideos {
  video_id SERIAL PK
  title VARCHAR(255)
  url TEXT
  course_id INT
}

// Relaciones
Ref: "Courses"."teacher_id" < "Users"."user_id"
Ref: "CourseVideos"."course_id" < "Courses"."course_id"
Ref: "UserRole"."user_id" < "Users"."user_id"
Ref: "UserRole"."role_id" < "Roles"."role_id"


///////////////////////////////////////////////////////////////////////////////////////////////////////////////

-- Creando las tablas

CREATE TABLE Roles (
    role_id SERIAL PRIMARY KEY,
    name VARCHAR(50) UNIQUE NOT NULL
);

CREATE TABLE Users (
    user_id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    age INT NOT NULL
);

CREATE TABLE UserRole (
    user_id INT REFERENCES Users(user_id),
    role_id INT REFERENCES Roles(role_id),
    PRIMARY KEY (user_id, role_id)
);

CREATE TABLE Categories (
    category_id SERIAL PRIMARY KEY,
    name VARCHAR(100) UNIQUE NOT NULL
);

CREATE TABLE Courses (
    course_id SERIAL PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    description TEXT NOT NULL,
    level VARCHAR(50) NOT NULL,
    teacher_id INT REFERENCES Users(user_id)
);

CREATE TABLE CourseVideos (
    video_id SERIAL PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    url TEXT NOT NULL,
    course_id INT REFERENCES Courses(course_id)
);

-- Insertar registros para Roles
INSERT INTO Roles(name) VALUES('estudiante'), ('maestro'), ('administrador');

-- Insertar registros para Users
INSERT INTO Users(name, email, password, age) VALUES('Juan Pérez', 'juan.perez@email.com', 'contraseña123', 25), ('María García', 'maria.garcia@email.com', 'contraseña456', 30);

-- Insertar registros para UserRole (asignando roles a los usuarios)
INSERT INTO UserRole(user_id, role_id) VALUES(1, 1), (2, 2);

-- Insertar registros para Categories
INSERT INTO Categories(name) VALUES('Programación'), ('Diseño');

-- Insertar registros para Courses
INSERT INTO Courses(title, description, level, teacher_id) VALUES('Introducción a Python', 'Curso básico de programación en Python', 'principiante', 2), ('Diseño Avanzado', 'Curso sobre conceptos avanzados de diseño', 'avanzado', 2);

-- Insertar registros para CourseVideos
INSERT INTO CourseVideos(title, url, course_id) VALUES('Básicos de Python', 'https://url1.com', 1), ('Principios de Diseño', 'https://url2.com', 2);

