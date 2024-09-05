  model {
        user_arrendatario = person "Arrendatario" {
            description "Persona que alquila vehículos."
        }
        user_dueno = person "Dueño de Vehículo" {
            description "Persona que publica vehículos para alquiler."
        }
        driveNow = softwareSystem "DriveNow" {
            description "Aplicación para la renta de vehículos."
        }
        container_web = container "Aplicación Web" {
            description "Frontend web para los usuarios."
            technology "React.js"
        }
        
  container_movil = container "Aplicación Móvil" {
            description "Frontend móvil para los usuarios."
            technology "Flutter"
        }
        container_api = container "API Gateway" {
            description "Punto central de entrada para las aplicaciones web y móvil."
            technology "Nginx, REST API"
        }
        container_gestion_vehiculos = container "Microservicio de Gestión de Vehículos" {
            description "Gestión de publicación, búsqueda y reserva de vehículos."
            technology "Spring Boot"
        }
        container_gestion_usuarios = container "Microservicio de Gestión de Usuarios" {
            description "Gestión de los usuarios (arrendatarios y dueños)."
            technology "Spring Boot"
        }
        container_pagos = container "Microservicio de Pagos" {
            description "Gestión de los pagos por los alquileres."
            technology "Spring Boot"
        }
        container_soporte = container "Microservicio de Atención al Cliente" {
            description "Módulo que gestiona el soporte y la atención al cliente."
            technology "Spring Boot"
        }
        container_seguridad = container "Microservicio de Seguridad" {
            description "Gestión de autenticación y autorización."
            technology "Spring Boot"
        }
        container_db_vehiculos = container "Base de Datos de Vehículos" {
            description "Almacena la información de los vehículos."
            technology "MySQL"
        }
        // Relaciones
        user_arrendatario -> container_web "Usa"
        user_arrendatario -> container_movil "Usa"
        user_dueno -> container_web "Usa"
        user_dueno -> container_movil "Usa"
        container_web -> container_api "Solicitudes"
        container_movil -> container_api "Solicitudes"
        container_api -> container_gestion_vehiculos "Opera"
        container_api -> container_gestion_usuarios "Gestiona"
        container_api -> container_pagos "Procesa"
        container_api -> container_soporte "Asiste"
        container_api -> container_seguridad "Autentica"
        container_gestion_vehiculos -> container_db_vehiculos "Lectura/Escritura"
    }
    views {
        container driveNow {
            include *
            autolayout lr
        }
        theme default
    }
    styles {
        element {
            shape roundedBox
        }
        container {
            background #438DD5
            color white
        }
        database {
            shape cylinder
        }
        person {
            background #08427B
            color white
            shape person
        }
    }
}
