Resumen del proyecto — PhishGuard

Problema que resuelve: el phishing es el fraude digital más extendido entre la población española (SMS/emails falsos de Correos, bancos, etc.). La plataforma ayuda a cualquier usuario a verificar si un mensaje sospechoso es phishing antes de hacer clic.

Qué es

Una plataforma web de dos partes conectadas:

Producto (cara pública): el usuario pega un mensaje, enlace o cabeceras de email sospechoso, y el sistema devuelve un veredicto ("alto riesgo", "sospechoso", "parece legítimo") con explicación de qué señales detectó.
Laboratorio (infraestructura ASIR): un entorno aislado en Proxmox con servidor de correo propio (Postfix/Dovecot), donde generáis vuestros propios casos de prueba de forma controlada y ética, sin afectar a terceros.
Cómo analiza el phishing

Motor de reglas/scoring (no IA, por transparencia y porque es lo que de verdad podéis explicar ante el tribunal): cada señal suma puntos de riesgo — antigüedad del dominio (WHOIS), typosquatting, acortadores de URL, fallos en SPF/DKIM/DMARC, frases de urgencia en el texto, peticiones directas de datos bancarios. La suma total da el veredicto. Opcionalmente, como extra, se puede comparar contra una API de IA (LLM) para mostrar criterio sin depender de ella como base.

Arquitectura técnica
Capa	Tecnología
Hipervisor	Proxmox VE
SO	Debian/Ubuntu Server
Frontend	React/Vue.js
Backend	Python (Flask/FastAPI)
Base de datos	PostgreSQL
Servidor web	Nginx + TLS (Let's Encrypt)
Correo (lab)	Postfix + Dovecot
DNS	BIND9/dnsmasq, SPF/DKIM/DMARC
Red	iptables/nftables (segmentación lab/producción)
Protección pública	Cloudflare
Funcionalidades (por prioridad)
Altas: registro/login con roles, análisis de mensajes, verificación de dominios, laboratorio de correo aislado.
Medias: configuración SPF/DKIM/DMARC en el lab, histórico de análisis, panel admin con estadísticas.
Bajas (extras si hay tiempo): informes en PDF, simulación de campañas educativas de concienciación, extensión de navegador.
Planning

6 fases siguiendo el documento de la FP: briefing (sept) → arquitectura/diseño (1-11 oct) → memoria en paralelo todo el curso → ejecución en 4 sprints (15 oct-9 nov: infraestructura, backend+lab, motor de análisis+frontend, funcionalidades extra) → control (17-20 nov) → presentación (3 dic). Gestión con GitHub (código + Projects para tareas) y GitBook/Markdown para la memoria.

Equipo

Abdellah Chahmi Bahaqqy y Eric Reinaldo Salvador, ambos con perfil técnico en redes y seguridad, complementarios en soft skills (comunicación/responsabilidad y iniciativa/adaptabilidad respectivamente).
