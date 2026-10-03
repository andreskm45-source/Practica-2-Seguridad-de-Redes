# Practica-2-Seguridad-de-Redes
# Laboratorio de Seguridad de Redes: VPN Site-to-Site (Fortinet & Cisco)

**Autor:** Rafael Andrés Reyes De La Cruz (2025-0784)
**Institución:** Instituto Tecnológico de Las Américas (ITLA)

https://itlaedudo-my.sharepoint.com/:v:/g/personal/20250784_itla_edu_do/IQByh82V_i31TbVWOpZOahuqAapxrHRyw_pSO5SjFGPLzdk?e=QLoAeA&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0%3D

## Propósito del Laboratorio
Este proyecto tiene como objetivo diseñar, implementar y validar canales de comunicación seguros (túneles IPsec Site-to-Site) entre múltiples sedes a través de una infraestructura de red pública simulada (ISP). La práctica demuestra el aislamiento del tráfico corporativo, garantizando que la comunicación entre las VLANs de usuarios y los servidores web fluya de manera exclusiva y cifrada a través de la VPN. Si el túnel cae, la comunicación se interrumpe por completo, confirmando la ausencia de fugas de datos hacia Internet.

---

## Infraestructura 1: Ecosistema Fortinet (FortiGate a FortiGate)

Esta topología establece un túnel IPsec entre dos firewalls FortiGate utilizando las herramientas de interfaz gráfica (GUI)[cite: 24].

<img width="594" height="427" alt="image" src="https://github.com/user-attachments/assets/76f451cd-b120-4140-97bb-42ac1e7fc4dd" />


### Parámetros de Red
| Componente | Subred / IP | Interfaz / Función |
| :--- | :--- | :--- |
| **Usuarios (Sede A)** | `10.7.84.0/25` | VLAN 10 (con servidor DHCP activo) |
| **Servidor Web (Sede B)** | `10.7.84.128/28` | Puerto físico dedicado |
| **Gateway FortiGate A** | IP Pública Dinámica | WAN / NAT de salida |
| **Gateway FortiGate B** | IP Pública Dinámica | WAN / NAT de salida |

### Validaciones Realizadas
*   ✅ Configuración de políticas de firewall con NAT deshabilitado para el tráfico interno.
*   ✅ Enrutamiento estático hacia la interfaz virtual del túnel IPsec.
*   ✅ Prueba de conectividad mediante `tracepath` desde el cliente Ubuntu hacia el servidor HTTPs, evidenciando saltos exclusivos a través de la VPN.
