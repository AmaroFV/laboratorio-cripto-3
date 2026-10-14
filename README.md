# Laboratorio 3 — Criptografía y Seguridad en Redes (UDP)

Auditoría del **hash de contraseñas calculado en el cliente** en un sitio web real
y ataque **Pass the Hash (PtH)** interceptando el login con Burp Suite.

- **Ramo:** Criptografía y Seguridad en Redes — Escuela de Informática y
  Telecomunicaciones, Universidad Diego Portales.
- **Autor:** Amaro Figueroa (AmaroFV)
- **Sitio auditado:** SA 4x4 Community Forum
  (<https://www.4x4community.co.za/forum/>), vBulletin 4.2.5 detrás de Cloudflare.

## Resultado

| Punto | Hallazgo |
|-------|----------|
| Hash en el registro | MD5 sin sal, calculado en el navegador (`password_md5`) |
| Hash en el login | MD5 sin sal ni nonce (`vb_login_md5password`), mismo valor que en el registro |
| Hash desde la consola | `hex_md5("Lab3Cripto2026")` → `2a70467ad486f13d79e97b70fc7db373` |
| Intercepción | Burp Suite (navegador integrado + regla de intercepción por dominio) |
| Pass the Hash | Login con contraseña incorrecta + hash real → sesión iniciada |
| Política de privacidad | <https://www.4x4community.co.za/forum/privacy.php> — no menciona contraseñas |

Al terminar se cambió la contraseña de la cuenta; la contraseña del laboratorio
y su hash ya no permiten iniciar sesión.

## Estructura del repositorio

```
lab03_informe.tex          Informe final (fuente LaTeX, plantilla del ramo)
enunciado_original.pdf     Enunciado del laboratorio
actividades/               Capturas de pantalla usadas en el informe
├── registro_*.png         Formulario y POST del registro (DevTools)
├── login_*.png            Formulario, POST y resultado del login
├── consola_hex_md5.png    Generación del hash desde la consola
├── burp_intercept_*.png   Intercepción del login con Burp Suite
├── burp_pth_*.png         Petición modificada y login exitoso (PtH)
├── burp_history_*.png     Historial de Burp: petición original vs. editada
├── politica_privacidad.png
├── cambio_password_*.png  Formulario de cambio de contraseña (también MD5)
├── correo_reset_password.png
└── login_password_lab_rechazada.png
```
