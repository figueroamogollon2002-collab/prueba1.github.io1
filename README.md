index.html
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>El Chimbador - Viaja con Estilo</title>
<style>
    * { margin:0; padding:0; box-sizing:border-box; }
    body { font-family:-apple-system,BlinkMacSystemFont,'Segoe UI','Roboto','Oxygen','Ubuntu',sans-serif; background:#000; min-height:100vh; overflow-x:hidden; position:relative; }

    /* Fondos y partículas */
    .gradient-bg{position:fixed;width:100%;height:100%;background:linear-gradient(45deg,#0f0c29,#302b63,#24243e);z-index:0;}
    .gradient-overlay{position:fixed;width:100%;height:100%;background:radial-gradient(circle at 20% 50%, rgba(120,119,198,0.4), transparent 50%),radial-gradient(circle at 80% 80%, rgba(252,70,107,0.4), transparent 50%); z-index:1;animation:pulse 8s ease-in-out infinite;}
    @keyframes pulse{0%,100%{opacity:1;}50%{opacity:0.7;}}
    .particle{position:fixed;background:rgba(255,255,255,0.1);border-radius:50%;animation:float-particle 15s infinite ease-in-out; z-index:2;}
    @keyframes float-particle{0%,100%{transform:translateY(0) translateX(0);opacity:0;}10%{opacity:1;}90%{opacity:1;}100%{transform:translateY(-100vh) translateX(50px);opacity:0;}}

    /* Contenedores principales */
    .main-container { position:relative; z-index:10; display:grid; grid-template-columns:1fr 1fr; min-height:100vh; transition: all 0.5s; }
    .hero-section { display:flex; flex-direction:column; justify-content:center; padding:80px 100px; position:relative; }
    .hero-content { max-width:600px; animation:fadeInLeft 1s ease-out; }
    @keyframes fadeInLeft{from{opacity:0;transform:translateX(-40px);}to{opacity:1;transform:translateX(0);}}

    .logo-badge { display:inline-flex; align-items:center; gap:12px; background:rgba(255,255,255,0.1); backdrop-filter:blur(10px); padding:12px 24px; border-radius:50px; margin-bottom:32px; border:1px solid rgba(255,255,255,0.2);}
    .logo-icon { width:40px;height:40px;background:linear-gradient(135deg,#667eea 0%,#764ba2 100%); border-radius:50%; display:flex; align-items:center; justify-content:center; font-size:22px; animation:rotate-slow 20s linear infinite;}
    @keyframes rotate-slow{from{transform:rotate(0deg);}to{transform:rotate(360deg);}}
    .logo-text{font-size:20px;font-weight:700;color:#fff;letter-spacing:-0.5px;}
    .hero-title{font-size:72px;font-weight:900;color:#fff;line-height:1.1;margin-bottom:24px;letter-spacing:-2px;}
    .hero-title .gradient-text{background:linear-gradient(135deg,#667eea 0%,#764ba2 100%);-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;}
    .hero-subtitle{font-size:22px;color:rgba(255,255,255,0.7);line-height:1.6;margin-bottom:48px;}
    .features-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:24px;margin-top:60px;}
    .feature-card{background:rgba(255,255,255,0.05);backdrop-filter:blur(10px);border:1px solid rgba(255,255,255,0.1);border-radius:16px;padding:24px;transition:all 0.3s; animation:fadeInUp 0.6s ease-out backwards;}
    .feature-card:hover{background:rgba(255,255,255,0.08);transform:translateY(-4px);border-color:rgba(255,255,255,0.2);}
    .feature-card:nth-child(1){animation-delay:0.2s;} .feature-card:nth-child(2){animation-delay:0.3s;} .feature-card:nth-child(3){animation-delay:0.4s;}
    @keyframes fadeInUp{from{opacity:0;transform:translateY(20px);}to{opacity:1;transform:translateY(0);}}
    .feature-icon{font-size:32px;margin-bottom:12px;}
    .feature-title{font-size:16px;font-weight:600;color:#fff;margin-bottom:4px;}
    .feature-desc{font-size:13px;color:rgba(255,255,255,0.6);line-height:1.5;}
    .social-proof{display:flex;gap:32px;margin-top:48px;}
    .stat{text-align:center;}
    .stat-number{font-size:36px;font-weight:700;color:#fff;margin-bottom:4px;}
    .stat-label{font-size:14px;color:rgba(255,255,255,0.6);}

    /* Auth card (login/registro) */
    .auth-section { display:flex; align-items:center; justify-content:center; padding:80px 60px; position:relative; }
    .auth-card, .login-card { background:rgba(255,255,255,0.08); backdrop-filter:blur(30px); border-radius:32px; padding:56px 48px; border:1px solid rgba(255,255,255,0.15); box-shadow:0 32px 64px rgba(0,0,0,0.5); max-width:480px; width:100%; animation:fadeInRight 1s ease-out; position:absolute; top:50%; left:50%; transform:translate(-50%, -50%); display:none; z-index:20;}
    .auth-card.active, .login-card.active { display:block; }

    @keyframes fadeInRight{from{opacity:0;transform:translateX(40px);}to{opacity:1;transform:translateX(0);} }

    .auth-header, .header { text-align:center; margin-bottom:40px; }
    .auth-title, .title { font-size:32px;font-weight:700;color:#fff;margin-bottom:8px; }
    .auth-subtitle, .subtitle { font-size:16px;color:rgba(255,255,255,0.6); }
    .button-group { display:flex; flex-direction:column; gap:16px; }
    .btn{position:relative;padding:20px 32px;border:none;border-radius:16px;font-size:17px;font-weight:600;cursor:pointer;transition:all 0.3s; overflow:hidden; display:flex; align-items:center; justify-content:center; gap:12px;}
    .btn::before{content:'';position:absolute;top:50%;left:50%;width:0;height:0;border-radius:50%;background:rgba(255,255,255,0.2);transform:translate(-50%, -50%);transition:width 0.6s,height 0.6s;}
    .btn:hover::before{width:400px;height:400px;}
    .btn:active{transform:scale(0.98);}
    .btn-content{position:relative; z-index:1; display:flex; align-items:center; gap:10px;}
    .btn-icon{font-size:22px;}
    .btn-primary{background:linear-gradient(135deg,#667eea 0%,#764ba2 100%);color:white;box-shadow:0 8px 24px rgba(102,126,234,0.4);}
    .btn-primary:hover{box-shadow:0 12px 32px rgba(102,126,234,0.6);transform:translateY(-3px);}
    .btn-secondary{background:rgba(255,255,255,0.1);color:white;border:2px solid rgba(255,255,255,0.2);backdrop-filter:blur(10px);}
    .btn-secondary:hover{background:rgba(255,255,255,0.15);border-color:rgba(255,255,255,0.3);transform:translateY(-3px);}

    /* Login form */
    .form-group{margin-bottom:24px;}
    .form-label{display:block;color:rgba(255,255,255,0.9);font-size:14px;font-weight:600;margin-bottom:8px;}
    .input-wrapper{position:relative;}
    .input-icon{position:absolute;left:16px;top:50%;transform:translateY(-50%);font-size:20px;color:rgba(255,255,255,0.5);}
    .form-input{width:100%;padding:16px 16px 16px 50px;background:rgba(255,255,255,0.1);border:2px solid rgba(255,255,255,0.1);border-radius:12px;color:white;font-size:16px;transition:all 0.3s;backdrop-filter:blur(10px);}
    .form-input::placeholder{color:rgba(255,255,255,0.4);}
    .form-input:focus{outline:none;background:rgba(255,255,255,0.15);border-color:rgba(102,126,234,0.6);box-shadow:0 0 0 4px rgba(102,126,234,0.1);}

    /* Botón login */
    .btn-login{width:100%;padding:18px;background:linear-gradient(135deg,#667eea 0%,#764ba2 100%);border:none;border-radius:12px;color:white;font-size:17px;font-weight:600;cursor:pointer;transition:all 0.3s;box-shadow:0 8px 24px rgba(102,126,234,0.4);position:relative; overflow:hidden;}
    .btn-login::before{content:'';position:absolute;top:50%;left:50%;width:0;height:0;border-radius:50%;background:rgba(255,255,255,0.2);transform:translate(-50%, -50%);transition:width 0.6s,height 0.6s;}
    .btn-login:hover::before{width:400px;height:400px;}
    .btn-login:hover{box-shadow:0 12px 32px rgba(102,126,234,0.6);transform:translateY(-2px);}
    .btn-login:active{transform:translateY(0);}

    .back-button{position:absolute;top:40px;left:40px;background:rgba(255,255,255,0.1);backdrop-filter:blur(10px);border:1px solid rgba(255,255,255,0.2);color:white;padding:12px 24px;border-radius:12px;cursor:pointer;font-size:15px;font-weight:600;display:flex;align-items:center;gap:8px;transition:all 0.3s;z-index:30;}
    .back-button:hover{background:rgba(255,255,255,0.15);transform:translateX(-4px);}
</style>
</head>
<body>
<div class="gradient-bg"></div>
<div class="gradient-overlay"></div>
<div id="particlesContainer"></div>

<div class="main-container" id="mainContainer">
    <!-- Hero -->
    <div class="hero-section">
        <div class="hero-content">
            <div class="logo-badge">
                <div class="logo-icon">🚌</div>
                <span class="logo-text">El Chimbador</span>
            </div>

            <h1 class="hero-title">
                Viaja con<br>
                <span class="gradient-text">Estilo y Comodidad</span>
            </h1>
            <p class="hero-subtitle">La forma más moderna de reservar tus viajes.</p>

            <div class="social-proof">
                <div class="stat"><div class="stat-number">10K+</div><div class="stat-label">Viajes realizados</div></div>
                <div class="stat"><div class="stat-number">4.9⭐</div><div class="stat-label">Calificación</div></div>
                <div class="stat"><div class="stat-number">50+</div><div class="stat-label">Rutas disponibles</div></div>
            </div>

            <div class="features-grid">
                <div class="feature-card"><div class="feature-icon">⚡</div><div class="feature-title">Reserva Rápida</div><div class="feature-desc">En segundos puedes reservar tu asiento</div></div>
                <div class="feature-card"><div class="feature-icon">🔒</div><div class="feature-title">100% Seguro</div><div class="feature-desc">Viaja con tranquilidad</div></div>
                <div class="feature-card"><div class="feature-icon">💎</div><div class="feature-title">Mejor Precio</div><div class="feature-desc">Tarifas justas y transparentes</div></div>
            </div>

            <div class="button-group" style="margin-top:60px;">
                <button class="btn btn-primary" onclick="showLogin()">👤 Iniciar Sesión</button>
                <button class="btn btn-secondary" onclick="showRegister()">✨ Crear Cuenta</button>
            </div>
        </div>
    </div>
</div>

<!-- Login Card -->
<div class="login-card" id="loginCard">
    <div class="back-button" onclick="volverHero()">← Volver</div>
    <div class="header">
        <div class="logo-icon">🚌</div>
        <h1 class="title">Bienvenido de nuevo</h1>
        <p class="subtitle">Ingresa a tu cuenta para continuar</p>
    </div>
    <form onsubmit="handleLogin(event)">
        <div class="form-group">
            <label class="form-label">Correo o Usuario</label>
            <div class="input-wrapper">
                <span class="input-icon">📧</span>
                <input type="text" class="form-input" placeholder="usuario@ejemplo.com" required>
            </div>
        </div>
        <div class="form-group">
            <label class="form-label">Contraseña</label>
            <div class="input-wrapper">
                <span class="input-icon">🔒</span>
                <input type="password" class="form-input" placeholder="••••••••" required>
            </div>
        </div>
        <button type="submit" class="btn-login">Iniciar Sesión</button>
    </form>
</div>

<script>
    // Crear partículas
    function createParticles(){
        const container = document.getElementById('particlesContainer');
        for(let i=0;i<40;i++){
            const p=document.createElement('div');p.className='particle';
            const size=Math.random()*4+2;p.style.width=size+'px';p.style.height=size+'px';
            p.style.left=Math.random()*100+'%';
            p.style.animationDelay=Math.random()*15+'s';
            p.style.animationDuration=(Math.random()*10+10)+'s';
            container.appendChild(p);
        }
    }
    createParticles();

    function showLogin(){ document.getElementById('loginCard').classList.add('active'); document.getElementById('mainContainer').style.opacity='0.2'; }
    function showRegister(){ alert('Redirigiendo a registro...'); }
    function volverHero(){ document.getElementById('loginCard').classList.remove('active'); document.getElementById('mainContainer').style.opacity='1'; }
    function handleLogin(e){ e.preventDefault(); alert('Iniciando sesión...'); }
</script>
</body>
</html>
