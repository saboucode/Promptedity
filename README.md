<!doctype html>
<html lang="en" class="h-full">
 <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Promptedity - The Intelligence Behind Every Prompt</title>
  <script src="https://cdn.tailwindcss.com/3.4.17"></script>
  <script src="/_sdk/element_sdk.js"></script>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&amp;display=swap" rel="stylesheet">
  <style>
    * { font-family: 'Inter', sans-serif; }
    
    :root {
      --cyan: #00f5ff;
      --lime: #a3ff00;
      --purple: #8b5cf6;
      --dark: #0a0a0f;
      --darker: #050508;
    }
    
    html, body { 
      height: 100%; 
      background: var(--darker);
      overflow-x: hidden;
    }
    
    .main-wrapper {
      height: 100%;
      width: 100%;
      overflow-y: auto;
      overflow-x: hidden;
      background: var(--darker);
    }
    
    /* Neural Network Background */
    .neural-bg {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
      z-index: 0;
    }
    
    .neural-particle {
      position: absolute;
      width: 4px;
      height: 4px;
      background: var(--cyan);
      border-radius: 50%;
      opacity: 0.3;
      animation: float 20s infinite ease-in-out;
    }
    
    .neural-line {
      position: absolute;
      height: 1px;
      background: linear-gradient(90deg, transparent, var(--cyan), transparent);
      opacity: 0.1;
      animation: pulse-line 8s infinite;
    }
    
    @keyframes float {
      0%, 100% { transform: translate(0, 0) scale(1); opacity: 0.3; }
      25% { transform: translate(50px, -30px) scale(1.2); opacity: 0.5; }
      50% { transform: translate(-20px, 50px) scale(0.8); opacity: 0.2; }
      75% { transform: translate(30px, 20px) scale(1.1); opacity: 0.4; }
    }
    
    @keyframes pulse-line {
      0%, 100% { opacity: 0.05; transform: scaleX(0.5); }
      50% { opacity: 0.15; transform: scaleX(1); }
    }
    
    /* Glow Effects */
    .glow-cyan {
      box-shadow: 0 0 30px rgba(0, 245, 255, 0.5), 0 0 60px rgba(0, 245, 255, 0.3);
    }
    
    .glow-lime {
      box-shadow: 0 0 30px rgba(163, 255, 0, 0.5), 0 0 60px rgba(163, 255, 0, 0.3);
    }
    
    .text-glow-cyan {
      text-shadow: 0 0 20px rgba(0, 245, 255, 0.8), 0 0 40px rgba(0, 245, 255, 0.4);
    }
    
    .text-glow-lime {
      text-shadow: 0 0 20px rgba(163, 255, 0, 0.8), 0 0 40px rgba(163, 255, 0, 0.4);
    }
    
    /* Glassmorphism */
    .glass-card {
      background: rgba(255, 255, 255, 0.03);
      backdrop-filter: blur(20px);
      border: 1px solid rgba(255, 255, 255, 0.08);
      transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
    }
    
    .glass-card:hover {
      background: rgba(255, 255, 255, 0.06);
      border-color: rgba(0, 245, 255, 0.3);
      transform: translateY(-8px);
      box-shadow: 0 20px 60px rgba(0, 245, 255, 0.15);
    }
    
    /* Button Styles */
    .btn-cyan {
      background: linear-gradient(135deg, #00f5ff, #00c8d4);
      color: #000;
      font-weight: 700;
      transition: all 0.3s ease;
    }
    
    .btn-cyan:hover {
      transform: translateY(-3px);
      box-shadow: 0 10px 40px rgba(0, 245, 255, 0.5);
    }
    
    .btn-lime {
      background: linear-gradient(135deg, #a3ff00, #7acc00);
      color: #000;
      font-weight: 700;
      transition: all 0.3s ease;
    }
    
    .btn-lime:hover {
      transform: translateY(-3px);
      box-shadow: 0 10px 40px rgba(163, 255, 0, 0.5);
    }
    
    .btn-outline {
      background: transparent;
      border: 2px solid var(--cyan);
      color: var(--cyan);
      transition: all 0.3s ease;
    }
    
    .btn-outline:hover {
      background: var(--cyan);
      color: #000;
    }
    
    /* Prompt Card Styles */
    .prompt-card {
      position: relative;
      overflow: hidden;
    }
    
    .prompt-card::before {
      content: '';
      position: absolute;
      top: 0;
      left: -100%;
      width: 100%;
      height: 100%;
      background: linear-gradient(90deg, transparent, rgba(255,255,255,0.1), transparent);
      transition: left 0.5s ease;
    }
    
    .prompt-card:hover::before {
      left: 100%;
    }
    
    /* Battle Arena */
    .battle-card {
      position: relative;
      animation: battle-pulse 3s infinite;
    }
    
    @keyframes battle-pulse {
      0%, 100% { box-shadow: 0 0 20px rgba(139, 92, 246, 0.3); }
      50% { box-shadow: 0 0 40px rgba(139, 92, 246, 0.6); }
    }
    
    /* Scroll Animations */
    .fade-up {
      opacity: 0;
      transform: translateY(40px);
      animation: fadeUp 0.8s ease forwards;
    }
    
    @keyframes fadeUp {
      to { opacity: 1; transform: translateY(0); }
    }
    
    .delay-1 { animation-delay: 0.1s; }
    .delay-2 { animation-delay: 0.2s; }
    .delay-3 { animation-delay: 0.3s; }
    .delay-4 { animation-delay: 0.4s; }
    .delay-5 { animation-delay: 0.5s; }
    .delay-6 { animation-delay: 0.6s; }
    
    /* Logo Animation */
    .logo-glow {
      animation: logo-pulse 4s infinite;
    }
    
    @keyframes logo-pulse {
      0%, 100% { filter: drop-shadow(0 0 20px rgba(0, 245, 255, 0.8)); }
      50% { filter: drop-shadow(0 0 40px rgba(0, 245, 255, 1)); }
    }
    
    /* Floating Bubbles */
    .bubble {
      position: absolute;
      border-radius: 20px;
      background: rgba(255, 255, 255, 0.02);
      border: 1px solid rgba(255, 255, 255, 0.05);
      backdrop-filter: blur(10px);
      animation: bubble-float 15s infinite ease-in-out;
    }
    
    @keyframes bubble-float {
      0%, 100% { transform: translate(0, 0) rotate(0deg); }
      33% { transform: translate(20px, -30px) rotate(5deg); }
      66% { transform: translate(-15px, 20px) rotate(-5deg); }
    }
    
    /* Vote Bar Animation */
    .vote-bar {
      transition: width 1s ease-out;
    }
    
    /* Gradient Text */
    .gradient-text {
      background: linear-gradient(135deg, #00f5ff, #a3ff00);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }
    
    /* Section Divider */
    .section-divider {
      height: 1px;
      background: linear-gradient(90deg, transparent, rgba(0, 245, 255, 0.3), transparent);
    }
    
    /* Input Styles */
    .input-glow:focus {
      outline: none;
      border-color: var(--cyan);
      box-shadow: 0 0 20px rgba(0, 245, 255, 0.3);
    }
    
    /* RTL Toggle */
    .rtl-toggle {
      cursor: pointer;
      transition: all 0.3s ease;
    }
    
    .rtl-toggle:hover {
      color: var(--cyan);
    }
    
    /* Testimonial Avatar */
    .avatar-ring {
      background: linear-gradient(135deg, var(--cyan), var(--purple));
      padding: 3px;
      border-radius: 50%;
    }
    
    /* Stats Counter */
    .stat-number {
      font-variant-numeric: tabular-nums;
    }
  </style>
  <style>body { box-sizing: border-box; }</style>
  <script src="/_sdk/data_sdk.js" type="text/javascript"></script>
 </head>
 <body class="h-full bg-[#050508] text-white">
  <div class="main-wrapper"><!-- Neural Network Background -->
   <div class="neural-bg" id="neural-bg"></div><!-- Navigation -->
   <nav class="fixed top-0 left-0 right-0 z-50 px-6 py-4">
    <div class="max-w-7xl mx-auto flex items-center justify-between">
     <div class="flex items-center gap-3">
      <svg class="w-10 h-10 logo-glow" viewbox="0 0 100 100"><defs>
        <lineargradient id="logoGrad" x1="0%" y1="0%" x2="100%" y2="100%">
         <stop offset="0%" style="stop-color:#00f5ff" />
         <stop offset="100%" style="stop-color:#a3ff00" />
        </lineargradient>
       </defs> <path d="M20 15 L50 15 Q75 15 75 40 Q75 55 55 60 L45 60 L45 85 L20 85 Z" fill="url(#logoGrad)" opacity="0.9" /> <path d="M55 60 L70 75" stroke="#00f5ff" stroke-width="3" stroke-linecap="round" /> <path d="M75 40 L90 30" stroke="#a3ff00" stroke-width="2" stroke-linecap="round" /> <circle cx="90" cy="30" r="4" fill="#a3ff00" /> <circle cx="70" cy="75" r="4" fill="#00f5ff" /> <path d="M30 30 L35 30 M30 45 L40 45 M30 60 L35 60" stroke="#050508" stroke-width="2" stroke-linecap="round" />
      </svg><span class="text-xl font-bold tracking-tight">Promptedity</span>
     </div>
     <div class="hidden md:flex items-center gap-8"><a href="#features" class="text-gray-400 hover:text-white transition-colors text-sm font-medium">Features</a> <a href="#prompts" class="text-gray-400 hover:text-white transition-colors text-sm font-medium">Prompts</a> <a href="#battles" class="text-gray-400 hover:text-white transition-colors text-sm font-medium">Battles</a> <a href="#marketplace" class="text-gray-400 hover:text-white transition-colors text-sm font-medium">Marketplace</a> <button class="rtl-toggle text-gray-500 text-sm" onclick="toggleLanguage()">🌐 العربية</button>
     </div>
     <div class="flex items-center gap-3"><button class="btn-outline px-5 py-2 rounded-full text-sm hidden sm:block">Sign In</button> <button class="btn-cyan px-5 py-2 rounded-full text-sm">Get Started</button>
     </div>
    </div>
   </nav><!-- Hero Section -->
   <section class="relative min-h-screen flex items-center justify-center px-6 pt-20 overflow-hidden"><!-- Floating Bubbles -->
    <div class="bubble w-48 h-32 top-20 left-10 hidden lg:block" style="animation-delay: 0s;">
     <div class="p-4 text-xs text-gray-500"><span class="text-cyan-400">→</span> Write a viral tweet about...
     </div>
    </div>
    <div class="bubble w-56 h-36 top-32 right-20 hidden lg:block" style="animation-delay: -5s;">
     <div class="p-4 text-xs text-gray-500"><span class="text-lime-400">→</span> Generate code for a React...
     </div>
    </div>
    <div class="bubble w-44 h-28 bottom-32 left-20 hidden lg:block" style="animation-delay: -10s;">
     <div class="p-4 text-xs text-gray-500"><span class="text-purple-400">→</span> Create an image of...
     </div>
    </div>
    <div class="max-w-5xl mx-auto text-center relative z-10"><!-- Logo -->
     <div class="mb-8 fade-up">
      <svg class="w-32 h-32 mx-auto logo-glow" viewbox="0 0 100 100"><defs>
        <lineargradient id="heroLogoGrad" x1="0%" y1="0%" x2="100%" y2="100%">
         <stop offset="0%" style="stop-color:#00f5ff" />
         <stop offset="100%" style="stop-color:#a3ff00" />
        </lineargradient>
        <filter id="glow">
         <fegaussianblur stddeviation="3" result="coloredBlur" />
         <femerge>
          <femergenode in="coloredBlur" />
          <femergenode in="SourceGraphic" />
         </femerge>
        </filter>
       </defs> <path d="M20 10 L55 10 Q80 10 80 40 Q80 60 55 65 L40 65 L40 90 L20 90 Z" fill="url(#heroLogoGrad)" filter="url(#glow)" /> <path d="M55 65 L75 85" stroke="#00f5ff" stroke-width="4" stroke-linecap="round" filter="url(#glow)" /> <path d="M80 40 L95 25" stroke="#a3ff00" stroke-width="3" stroke-linecap="round" filter="url(#glow)" /> <circle cx="95" cy="25" r="5" fill="#a3ff00" filter="url(#glow)" /> <circle cx="75" cy="85" r="5" fill="#00f5ff" filter="url(#glow)" /> <path d="M32 28 L42 28 M32 45 L50 45 M32 62 L42 62" stroke="#050508" stroke-width="3" stroke-linecap="round" />
      </svg>
     </div><!-- Tagline -->
     <p class="text-cyan-400 text-sm font-medium tracking-[0.3em] uppercase mb-6 fade-up delay-1">The Intelligence Behind Every Prompt</p><!-- Headline -->
     <h1 id="hero-headline" class="text-5xl md:text-7xl lg:text-8xl font-black mb-6 leading-[0.95] fade-up delay-2"><span class="text-white">Master Every Prompt.</span><br><span class="gradient-text">Build the Future.</span></h1><!-- Subheadline -->
     <p id="hero-subheadline" class="text-xl md:text-2xl text-gray-400 mb-10 max-w-2xl mx-auto font-light fade-up delay-3">Discover, Edit, Battle &amp; Sell the world's most powerful AI prompts</p><!-- CTA Buttons -->
     <div class="flex flex-col sm:flex-row gap-4 justify-center fade-up delay-4"><button class="btn-cyan px-10 py-4 rounded-full text-lg glow-cyan"> Explore Prompts → </button> <button class="btn-lime px-10 py-4 rounded-full text-lg glow-lime"> Join the Movement – Free </button>
     </div><!-- Stats -->
     <div class="mt-16 grid grid-cols-3 gap-8 max-w-lg mx-auto fade-up delay-5">
      <div class="text-center">
       <div class="stat-number text-3xl font-bold text-white">
        50K+
       </div>
       <div class="text-gray-500 text-sm">
        Prompts
       </div>
      </div>
      <div class="text-center">
       <div class="stat-number text-3xl font-bold text-white">
        120K+
       </div>
       <div class="text-gray-500 text-sm">
        Users
       </div>
      </div>
      <div class="text-center">
       <div class="stat-number text-3xl font-bold text-white">
        $2M+
       </div>
       <div class="text-gray-500 text-sm">
        Earned
       </div>
      </div>
     </div>
    </div><!-- Scroll Indicator -->
    <div class="absolute bottom-8 left-1/2 -translate-x-1/2 animate-bounce">
     <svg class="w-6 h-6 text-gray-600" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 14l-7 7m0 0l-7-7m7 7V3" />
     </svg>
    </div>
   </section><!-- How It Works -->
   <section id="features" class="py-24 px-6 relative">
    <div class="section-divider mb-24"></div>
    <div class="max-w-6xl mx-auto">
     <div class="text-center mb-16">
      <p class="text-cyan-400 text-sm font-medium tracking-[0.2em] uppercase mb-4">Simple &amp; Powerful</p>
      <h2 class="text-4xl md:text-5xl font-bold">How It Works</h2>
     </div>
     <div class="grid md:grid-cols-4 gap-6"><!-- Step 1 -->
      <div class="glass-card rounded-3xl p-8 text-center fade-up">
       <div class="w-16 h-16 mx-auto mb-6 rounded-2xl bg-gradient-to-br from-cyan-500/20 to-cyan-500/5 flex items-center justify-center">
        <svg class="w-8 h-8 text-cyan-400" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
        </svg>
       </div>
       <div class="text-cyan-400 text-sm font-bold mb-2">
        01
       </div>
       <h3 class="text-xl font-bold mb-3">Discover</h3>
       <p class="text-gray-500 text-sm">Browse thousands of premium prompts for every AI model</p>
      </div><!-- Step 2 -->
      <div class="glass-card rounded-3xl p-8 text-center fade-up delay-1">
       <div class="w-16 h-16 mx-auto mb-6 rounded-2xl bg-gradient-to-br from-lime-500/20 to-lime-500/5 flex items-center justify-center">
        <svg class="w-8 h-8 text-lime-400" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z" />
        </svg>
       </div>
       <div class="text-lime-400 text-sm font-bold mb-2">
        02
       </div>
       <h3 class="text-xl font-bold mb-3">Edit</h3>
       <p class="text-gray-500 text-sm">Customize and optimize prompts with our AI editor</p>
      </div><!-- Step 3 -->
      <div class="glass-card rounded-3xl p-8 text-center fade-up delay-2">
       <div class="w-16 h-16 mx-auto mb-6 rounded-2xl bg-gradient-to-br from-purple-500/20 to-purple-500/5 flex items-center justify-center">
        <svg class="w-8 h-8 text-purple-400" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z" />
        </svg>
       </div>
       <div class="text-purple-400 text-sm font-bold mb-2">
        03
       </div>
       <h3 class="text-xl font-bold mb-3">Battle</h3>
       <p class="text-gray-500 text-sm">Compete with others to create the best prompts</p>
      </div><!-- Step 4 -->
      <div class="glass-card rounded-3xl p-8 text-center fade-up delay-3">
       <div class="w-16 h-16 mx-auto mb-6 rounded-2xl bg-gradient-to-br from-orange-500/20 to-orange-500/5 flex items-center justify-center">
        <svg class="w-8 h-8 text-orange-400" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
        </svg>
       </div>
       <div class="text-orange-400 text-sm font-bold mb-2">
        04
       </div>
       <h3 class="text-xl font-bold mb-3">Sell</h3>
       <p class="text-gray-500 text-sm">Monetize your best prompts in our marketplace</p>
      </div>
     </div>
    </div>
   </section><!-- Featured Prompts -->
   <section id="prompts" class="py-24 px-6 relative">
    <div class="section-divider mb-24"></div>
    <div class="max-w-6xl mx-auto">
     <div class="text-center mb-16">
      <p class="text-lime-400 text-sm font-medium tracking-[0.2em] uppercase mb-4">Top Rated</p>
      <h2 class="text-4xl md:text-5xl font-bold">Featured Prompts</h2>
     </div>
     <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-6"><!-- Marketing Prompt -->
      <div class="glass-card prompt-card rounded-3xl p-6 fade-up">
       <div class="flex items-start justify-between mb-4">
        <div class="w-12 h-12 rounded-xl bg-gradient-to-br from-pink-500 to-rose-600 flex items-center justify-center text-2xl">
         📈
        </div><span class="px-3 py-1 rounded-full bg-cyan-500/10 text-cyan-400 text-xs font-medium">GPT-4</span>
       </div>
       <h3 class="text-lg font-bold mb-2">Viral Marketing Copy</h3>
       <p class="text-gray-500 text-sm mb-4">Generate scroll-stopping ad copy that converts like crazy</p>
       <div class="flex items-center justify-between">
        <div class="flex items-center gap-2"><span class="text-yellow-400">★★★★★</span> <span class="text-gray-600 text-xs">4.9</span>
        </div><span class="text-lime-400 font-bold">$12.99</span>
       </div>
      </div><!-- Creative Prompt -->
      <div class="glass-card prompt-card rounded-3xl p-6 fade-up delay-1">
       <div class="flex items-start justify-between mb-4">
        <div class="w-12 h-12 rounded-xl bg-gradient-to-br from-violet-500 to-purple-600 flex items-center justify-center text-2xl">
         ✨
        </div><span class="px-3 py-1 rounded-full bg-purple-500/10 text-purple-400 text-xs font-medium">Claude</span>
       </div>
       <h3 class="text-lg font-bold mb-2">Creative Storyteller</h3>
       <p class="text-gray-500 text-sm mb-4">Craft compelling narratives with emotional depth</p>
       <div class="flex items-center justify-between">
        <div class="flex items-center gap-2"><span class="text-yellow-400">★★★★★</span> <span class="text-gray-600 text-xs">4.8</span>
        </div><span class="text-lime-400 font-bold">$9.99</span>
       </div>
      </div><!-- Coding Prompt -->
      <div class="glass-card prompt-card rounded-3xl p-6 fade-up delay-2">
       <div class="flex items-start justify-between mb-4">
        <div class="w-12 h-12 rounded-xl bg-gradient-to-br from-green-500 to-emerald-600 flex items-center justify-center text-2xl">
         💻
        </div><span class="px-3 py-1 rounded-full bg-lime-500/10 text-lime-400 text-xs font-medium">GPT-4</span>
       </div>
       <h3 class="text-lg font-bold mb-2">Senior Dev Assistant</h3>
       <p class="text-gray-500 text-sm mb-4">Write production-ready code with best practices</p>
       <div class="flex items-center justify-between">
        <div class="flex items-center gap-2"><span class="text-yellow-400">★★★★★</span> <span class="text-gray-600 text-xs">5.0</span>
        </div><span class="text-lime-400 font-bold">$19.99</span>
       </div>
      </div><!-- Image Prompt -->
      <div class="glass-card prompt-card rounded-3xl p-6 fade-up delay-3">
       <div class="flex items-start justify-between mb-4">
        <div class="w-12 h-12 rounded-xl bg-gradient-to-br from-blue-500 to-indigo-600 flex items-center justify-center text-2xl">
         🎨
        </div><span class="px-3 py-1 rounded-full bg-blue-500/10 text-blue-400 text-xs font-medium">Midjourney</span>
       </div>
       <h3 class="text-lg font-bold mb-2">Photorealistic Magic</h3>
       <p class="text-gray-500 text-sm mb-4">Create stunning photorealistic images effortlessly</p>
       <div class="flex items-center justify-between">
        <div class="flex items-center gap-2"><span class="text-yellow-400">★★★★★</span> <span class="text-gray-600 text-xs">4.9</span>
        </div><span class="text-lime-400 font-bold">$14.99</span>
       </div>
      </div><!-- Business Prompt -->
      <div class="glass-card prompt-card rounded-3xl p-6 fade-up delay-4">
       <div class="flex items-start justify-between mb-4">
        <div class="w-12 h-12 rounded-xl bg-gradient-to-br from-amber-500 to-orange-600 flex items-center justify-center text-2xl">
         📊
        </div><span class="px-3 py-1 rounded-full bg-orange-500/10 text-orange-400 text-xs font-medium">Gemini</span>
       </div>
       <h3 class="text-lg font-bold mb-2">Business Strategist</h3>
       <p class="text-gray-500 text-sm mb-4">Get MBA-level business insights instantly</p>
       <div class="flex items-center justify-between">
        <div class="flex items-center gap-2"><span class="text-yellow-400">★★★★★</span> <span class="text-gray-600 text-xs">4.7</span>
        </div><span class="text-lime-400 font-bold">$24.99</span>
       </div>
      </div><!-- Arabic Prompt -->
      <div class="glass-card prompt-card rounded-3xl p-6 fade-up delay-5">
       <div class="flex items-start justify-between mb-4">
        <div class="w-12 h-12 rounded-xl bg-gradient-to-br from-teal-500 to-cyan-600 flex items-center justify-center text-2xl">
         🌙
        </div><span class="px-3 py-1 rounded-full bg-cyan-500/10 text-cyan-400 text-xs font-medium">Grok</span>
       </div>
       <h3 class="text-lg font-bold mb-2">Arabic Content Pro</h3>
       <p class="text-gray-500 text-sm mb-4">Native Arabic content that resonates culturally</p>
       <div class="flex items-center justify-between">
        <div class="flex items-center gap-2"><span class="text-yellow-400">★★★★★</span> <span class="text-gray-600 text-xs">4.9</span>
        </div><span class="text-lime-400 font-bold">$11.99</span>
       </div>
      </div>
     </div>
     <div class="text-center mt-12"><button class="btn-outline px-8 py-3 rounded-full">View All Prompts →</button>
     </div>
    </div>
   </section><!-- Prompt Battles -->
   <section id="battles" class="py-24 px-6 relative">
    <div class="section-divider mb-24"></div>
    <div class="max-w-6xl mx-auto">
     <div class="text-center mb-16">
      <p class="text-purple-400 text-sm font-medium tracking-[0.2em] uppercase mb-4">Live Competition</p>
      <h2 class="text-4xl md:text-5xl font-bold mb-4">Prompt Battles</h2>
      <p class="text-gray-500 max-w-xl mx-auto">Watch prompts go head-to-head. Vote for winners. Rise to the top.</p>
     </div>
     <div class="glass-card battle-card rounded-3xl p-8 border-purple-500/30">
      <div class="flex items-center justify-between mb-8"><span class="px-4 py-2 rounded-full bg-red-500/20 text-red-400 text-sm font-bold flex items-center gap-2"> <span class="w-2 h-2 bg-red-500 rounded-full animate-pulse"></span> LIVE BATTLE </span> <span class="text-gray-500 text-sm">2,847 votes • Ends in 2h 34m</span>
      </div>
      <div class="grid md:grid-cols-2 gap-8"><!-- Challenger A -->
       <div class="bg-gradient-to-br from-cyan-500/10 to-transparent rounded-2xl p-6 border border-cyan-500/20">
        <div class="flex items-center gap-4 mb-4">
         <div class="w-12 h-12 rounded-full bg-gradient-to-br from-cyan-400 to-blue-500 flex items-center justify-center text-xl font-bold">
          A
         </div>
         <div>
          <h4 class="font-bold">UltraWriter Pro</h4>
          <p class="text-gray-500 text-sm">by @promptmaster</p>
         </div>
        </div>
        <p class="text-gray-400 text-sm mb-6">Advanced writing assistant with style adaptation and tone control...</p>
        <div class="mb-4">
         <div class="flex justify-between text-sm mb-2"><span class="text-cyan-400 font-bold">1,523 votes</span> <span class="text-gray-500">53%</span>
         </div>
         <div class="h-3 bg-gray-800 rounded-full overflow-hidden">
          <div class="vote-bar h-full bg-gradient-to-r from-cyan-500 to-cyan-400 rounded-full" style="width: 53%"></div>
         </div>
        </div><button class="w-full btn-cyan py-3 rounded-xl font-bold">Vote for A</button>
       </div><!-- Challenger B -->
       <div class="bg-gradient-to-br from-lime-500/10 to-transparent rounded-2xl p-6 border border-lime-500/20">
        <div class="flex items-center gap-4 mb-4">
         <div class="w-12 h-12 rounded-full bg-gradient-to-br from-lime-400 to-green-500 flex items-center justify-center text-xl font-bold">
          B
         </div>
         <div>
          <h4 class="font-bold">ContentGenius 3.0</h4>
          <p class="text-gray-500 text-sm">by @aiwhisperer</p>
         </div>
        </div>
        <p class="text-gray-400 text-sm mb-6">Multi-format content creator with SEO optimization built-in...</p>
        <div class="mb-4">
         <div class="flex justify-between text-sm mb-2"><span class="text-lime-400 font-bold">1,324 votes</span> <span class="text-gray-500">47%</span>
         </div>
         <div class="h-3 bg-gray-800 rounded-full overflow-hidden">
          <div class="vote-bar h-full bg-gradient-to-r from-lime-500 to-lime-400 rounded-full" style="width: 47%"></div>
         </div>
        </div><button class="w-full btn-lime py-3 rounded-xl font-bold">Vote for B</button>
       </div>
      </div>
     </div>
     <div class="text-center mt-12"><button class="btn-outline px-8 py-3 rounded-full border-purple-500 text-purple-400 hover:bg-purple-500 hover:text-white">Enter the Arena →</button>
     </div>
    </div>
   </section><!-- Why Promptedity -->
   <section class="py-24 px-6 relative">
    <div class="section-divider mb-24"></div>
    <div class="max-w-6xl mx-auto">
     <div class="text-center mb-16">
      <p class="text-cyan-400 text-sm font-medium tracking-[0.2em] uppercase mb-4">The Advantage</p>
      <h2 class="text-4xl md:text-5xl font-bold">Why Promptedity?</h2>
     </div>
     <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
      <div class="text-center fade-up">
       <div class="w-16 h-16 mx-auto mb-6 rounded-2xl bg-gradient-to-br from-cyan-500/20 to-cyan-500/5 flex items-center justify-center text-3xl">
        🚀
       </div>
       <h3 class="text-xl font-bold mb-3">10x Faster Results</h3>
       <p class="text-gray-500 text-sm">Skip the trial and error. Use battle-tested prompts that work.</p>
      </div>
      <div class="text-center fade-up delay-1">
       <div class="w-16 h-16 mx-auto mb-6 rounded-2xl bg-gradient-to-br from-lime-500/20 to-lime-500/5 flex items-center justify-center text-3xl">
        🎯
       </div>
       <h3 class="text-xl font-bold mb-3">AI Model Agnostic</h3>
       <p class="text-gray-500 text-sm">Works with ChatGPT, Claude, Gemini, Grok, Midjourney &amp; more.</p>
      </div>
      <div class="text-center fade-up delay-2">
       <div class="w-16 h-16 mx-auto mb-6 rounded-2xl bg-gradient-to-br from-purple-500/20 to-purple-500/5 flex items-center justify-center text-3xl">
        💰
       </div>
       <h3 class="text-xl font-bold mb-3">Earn Real Money</h3>
       <p class="text-gray-500 text-sm">Sell your prompts and build passive income streams.</p>
      </div>
      <div class="text-center fade-up delay-3">
       <div class="w-16 h-16 mx-auto mb-6 rounded-2xl bg-gradient-to-br from-orange-500/20 to-orange-500/5 flex items-center justify-center text-3xl">
        🏆
       </div>
       <h3 class="text-xl font-bold mb-3">Compete &amp; Level Up</h3>
       <p class="text-gray-500 text-sm">Battle other prompt engineers and climb the leaderboards.</p>
      </div>
      <div class="text-center fade-up delay-4">
       <div class="w-16 h-16 mx-auto mb-6 rounded-2xl bg-gradient-to-br from-pink-500/20 to-pink-500/5 flex items-center justify-center text-3xl">
        🌍
       </div>
       <h3 class="text-xl font-bold mb-3">Global Community</h3>
       <p class="text-gray-500 text-sm">Join 120,000+ prompt engineers worldwide. Arabic &amp; English.</p>
      </div>
      <div class="text-center fade-up delay-5">
       <div class="w-16 h-16 mx-auto mb-6 rounded-2xl bg-gradient-to-br from-blue-500/20 to-blue-500/5 flex items-center justify-center text-3xl">
        🔒
       </div>
       <h3 class="text-xl font-bold mb-3">Secure &amp; Private</h3>
       <p class="text-gray-500 text-sm">Your prompts are protected. Full ownership guaranteed.</p>
      </div>
     </div>
    </div>
   </section><!-- Testimonials -->
   <section class="py-24 px-6 relative">
    <div class="section-divider mb-24"></div>
    <div class="max-w-6xl mx-auto">
     <div class="text-center mb-16">
      <p class="text-lime-400 text-sm font-medium tracking-[0.2em] uppercase mb-4">Success Stories</p>
      <h2 class="text-4xl md:text-5xl font-bold">What People Say</h2>
     </div>
     <div class="grid md:grid-cols-3 gap-6">
      <div class="glass-card rounded-3xl p-8 fade-up">
       <div class="flex items-center gap-4 mb-6">
        <div class="avatar-ring">
         <div class="w-14 h-14 rounded-full bg-gradient-to-br from-purple-400 to-pink-500 flex items-center justify-center text-2xl">
          👨‍💻
         </div>
        </div>
        <div>
         <h4 class="font-bold">Alex Chen</h4>
         <p class="text-gray-500 text-sm">Tech Entrepreneur</p>
        </div>
       </div>
       <p class="text-gray-400 italic mb-4">"Promptedity changed how I work with AI. Made $15K selling prompts in my first month. This is the future."</p>
       <div class="text-yellow-400">
        ★★★★★
       </div>
      </div>
      <div class="glass-card rounded-3xl p-8 fade-up delay-1">
       <div class="flex items-center gap-4 mb-6">
        <div class="avatar-ring">
         <div class="w-14 h-14 rounded-full bg-gradient-to-br from-cyan-400 to-blue-500 flex items-center justify-center text-2xl">
          👩‍🎨
         </div>
        </div>
        <div>
         <h4 class="font-bold">Sarah Miller</h4>
         <p class="text-gray-500 text-sm">Creative Director</p>
        </div>
       </div>
       <p class="text-gray-400 italic mb-4">"The prompt battles are addictive! I've learned more about AI in 2 weeks than 2 years of tutorials."</p>
       <div class="text-yellow-400">
        ★★★★★
       </div>
      </div>
      <div class="glass-card rounded-3xl p-8 fade-up delay-2">
       <div class="flex items-center gap-4 mb-6">
        <div class="avatar-ring">
         <div class="w-14 h-14 rounded-full bg-gradient-to-br from-lime-400 to-green-500 flex items-center justify-center text-2xl">
          👨‍🔬
         </div>
        </div>
        <div>
         <h4 class="font-bold">Ahmed Hassan</h4>
         <p class="text-gray-500 text-sm">AI Researcher</p>
        </div>
       </div>
       <p class="text-gray-400 italic mb-4">"Finally a platform that understands Arabic. The quality of prompts here is unmatched. Absolute game-changer."</p>
       <div class="text-yellow-400">
        ★★★★★
       </div>
      </div>
     </div>
    </div>
   </section><!-- Marketplace Teaser -->
   <section id="marketplace" class="py-24 px-6 relative">
    <div class="section-divider mb-24"></div>
    <div class="max-w-4xl mx-auto">
     <div class="glass-card rounded-3xl p-12 text-center border-lime-500/20 bg-gradient-to-br from-lime-500/5 to-transparent">
      <div class="text-6xl mb-8">
       💎
      </div>
      <h2 class="text-4xl md:text-5xl font-bold mb-6">Turn Your <span class="gradient-text">Prompts</span> Into Profit</h2>
      <p class="text-xl text-gray-400 mb-8 max-w-2xl mx-auto">Join the marketplace revolution. Sell your best prompts to thousands of buyers worldwide. Set your prices. Earn 80% commission.</p>
      <div class="grid grid-cols-3 gap-8 mb-10 max-w-lg mx-auto">
       <div>
        <div class="text-3xl font-bold text-lime-400">
         80%
        </div>
        <div class="text-gray-500 text-sm">
         Commission
        </div>
       </div>
       <div>
        <div class="text-3xl font-bold text-cyan-400">
         50K+
        </div>
        <div class="text-gray-500 text-sm">
         Buyers
        </div>
       </div>
       <div>
        <div class="text-3xl font-bold text-purple-400">
         $2M+
        </div>
        <div class="text-gray-500 text-sm">
         Paid Out
        </div>
       </div>
      </div><button class="btn-lime px-10 py-4 rounded-full text-lg glow-lime">Start Selling Today →</button>
     </div>
    </div>
   </section><!-- Final CTA -->
   <section class="py-24 px-6 relative">
    <div class="section-divider mb-24"></div>
    <div class="max-w-4xl mx-auto text-center">
     <h2 id="cta-headline" class="text-4xl md:text-6xl font-bold mb-6">Ready to Level Up<br><span class="gradient-text">Your AI Game?</span></h2>
     <p id="cta-subtext" class="text-xl text-gray-400 mb-10 max-w-xl mx-auto">Join 120,000+ prompt engineers building the future of AI. Start free today.</p>
     <form id="signup-form" class="max-w-md mx-auto mb-8" onsubmit="handleSignup(event)">
      <div class="flex gap-3"><input type="email" placeholder="Enter your email" class="flex-1 px-6 py-4 rounded-full bg-white/5 border border-white/10 text-white placeholder-gray-500 input-glow" required> <button type="submit" class="btn-cyan px-8 py-4 rounded-full font-bold whitespace-nowrap"> Get Started </button>
      </div>
     </form>
     <p class="text-gray-600 text-sm">No credit card required • Free forever plan • Cancel anytime</p><!-- AI Model Logos -->
     <div class="mt-16">
      <p class="text-gray-600 text-sm mb-6">Works with all major AI models</p>
      <div class="flex flex-wrap justify-center items-center gap-8 opacity-50"><span class="text-2xl font-bold text-gray-500">ChatGPT</span> <span class="text-2xl font-bold text-gray-500">Claude</span> <span class="text-2xl font-bold text-gray-500">Gemini</span> <span class="text-2xl font-bold text-gray-500">Grok</span> <span class="text-2xl font-bold text-gray-500">Midjourney</span>
      </div>
     </div>
    </div>
   </section><!-- Footer -->
   <footer class="py-16 px-6 border-t border-white/5">
    <div class="max-w-6xl mx-auto">
     <div class="grid md:grid-cols-4 gap-12 mb-12">
      <div>
       <div class="flex items-center gap-3 mb-6">
        <svg class="w-8 h-8" viewbox="0 0 100 100"><path d="M20 15 L50 15 Q75 15 75 40 Q75 55 55 60 L45 60 L45 85 L20 85 Z" fill="url(#logoGrad)" /> <path d="M55 60 L70 75" stroke="#00f5ff" stroke-width="3" stroke-linecap="round" />
        </svg><span class="text-lg font-bold">Promptedity</span>
       </div>
       <p class="text-gray-500 text-sm">The Intelligence Behind Every Prompt</p>
      </div>
      <div>
       <h4 class="font-bold mb-4">Product</h4>
       <ul class="space-y-3 text-gray-500 text-sm">
        <li><a href="#" class="hover:text-white transition-colors">Explore Prompts</a></li>
        <li><a href="#" class="hover:text-white transition-colors">Prompt Battles</a></li>
        <li><a href="#" class="hover:text-white transition-colors">Marketplace</a></li>
        <li><a href="#" class="hover:text-white transition-colors">API</a></li>
       </ul>
      </div>
      <div>
       <h4 class="font-bold mb-4">Company</h4>
       <ul class="space-y-3 text-gray-500 text-sm">
        <li><a href="#" class="hover:text-white transition-colors">About</a></li>
        <li><a href="#" class="hover:text-white transition-colors">Blog</a></li>
        <li><a href="#" class="hover:text-white transition-colors">Careers</a></li>
        <li><a href="#" class="hover:text-white transition-colors">Contact</a></li>
       </ul>
      </div>
      <div>
       <h4 class="font-bold mb-4">Legal</h4>
       <ul class="space-y-3 text-gray-500 text-sm">
        <li><a href="#" class="hover:text-white transition-colors">Privacy Policy</a></li>
        <li><a href="#" class="hover:text-white transition-colors">Terms of Service</a></li>
        <li><a href="#" class="hover:text-white transition-colors">Cookie Policy</a></li>
       </ul>
      </div>
     </div>
     <div class="flex flex-col md:flex-row items-center justify-between pt-8 border-t border-white/5">
      <p class="text-gray-600 text-sm">© 2024 Promptedity. All rights reserved.</p>
      <div class="flex items-center gap-6 mt-4 md:mt-0"><a href="#" class="text-gray-500 hover:text-cyan-400 transition-colors">𝕏</a> <a href="#" class="text-gray-500 hover:text-cyan-400 transition-colors">LinkedIn</a> <a href="#" class="text-gray-500 hover:text-cyan-400 transition-colors">Discord</a> <a href="#" class="text-gray-500 hover:text-cyan-400 transition-colors">GitHub</a>
      </div>
     </div>
    </div>
   </footer>
  </div>
  <script>
    // Default configuration
    const defaultConfig = {
      hero_headline: "Master Every Prompt. Build the Future.",
      hero_subheadline: "Discover, Edit, Battle & Sell the world's most powerful AI prompts",
      cta_headline: "Ready to Level Up Your AI Game?",
      cta_subtext: "Join 120,000+ prompt engineers building the future of AI. Start free today.",
      primary_color: "#00f5ff",
      secondary_color: "#a3ff00",
      accent_color: "#8b5cf6",
      background_color: "#050508",
      text_color: "#ffffff"
    };
    
    // Initialize Elements SDK
    if (window.elementSdk) {
      window.elementSdk.init({
        defaultConfig,
        onConfigChange: async (config) => {
          // Update hero section
          const heroHeadline = document.getElementById('hero-headline');
          if (heroHeadline) {
            const text = config.hero_headline || defaultConfig.hero_headline;
            const parts = text.split('.');
            if (parts.length >= 2) {
              heroHeadline.innerHTML = `<span class="text-white">${parts[0]}.</span><br><span class="gradient-text">${parts.slice(1).join('.').trim()}</span>`;
            } else {
              heroHeadline.innerHTML = `<span class="gradient-text">${text}</span>`;
            }
          }
          
          const heroSubheadline = document.getElementById('hero-subheadline');
          if (heroSubheadline) {
            heroSubheadline.textContent = config.hero_subheadline || defaultConfig.hero_subheadline;
          }
          
          // Update CTA section
          const ctaHeadline = document.getElementById('cta-headline');
          if (ctaHeadline) {
            const text = config.cta_headline || defaultConfig.cta_headline;
            ctaHeadline.innerHTML = text.replace(/Your AI Game/g, '<span class="gradient-text">Your AI Game</span>');
          }
          
          const ctaSubtext = document.getElementById('cta-subtext');
          if (ctaSubtext) {
            ctaSubtext.textContent = config.cta_subtext || defaultConfig.cta_subtext;
          }
          
          // Update colors
          document.documentElement.style.setProperty('--cyan', config.primary_color || defaultConfig.primary_color);
          document.documentElement.style.setProperty('--lime', config.secondary_color || defaultConfig.secondary_color);
          document.documentElement.style.setProperty('--purple', config.accent_color || defaultConfig.accent_color);
        },
        mapToCapabilities: (config) => ({
          recolorables: [
            {
              get: () => config.background_color || defaultConfig.background_color,
              set: (value) => window.elementSdk.setConfig({ background_color: value })
            },
            {
              get: () => config.text_color || defaultConfig.text_color,
              set: (value) => window.elementSdk.setConfig({ text_color: value })
            },
            {
              get: () => config.primary_color || defaultConfig.primary_color,
              set: (value) => window.elementSdk.setConfig({ primary_color: value })
            },
            {
              get: () => config.secondary_color || defaultConfig.secondary_color,
              set: (value) => window.elementSdk.setConfig({ secondary_color: value })
            },
            {
              get: () => config.accent_color || defaultConfig.accent_color,
              set: (value) => window.elementSdk.setConfig({ accent_color: value })
            }
          ],
          borderables: [],
          fontEditable: undefined,
          fontSizeable: undefined
        }),
        mapToEditPanelValues: (config) => new Map([
          ["hero_headline", config.hero_headline || defaultConfig.hero_headline],
          ["hero_subheadline", config.hero_subheadline || defaultConfig.hero_subheadline],
          ["cta_headline", config.cta_headline || defaultConfig.cta_headline],
          ["cta_subtext", config.cta_subtext || defaultConfig.cta_subtext]
        ])
      });
    }
    
    // Create neural network background
    function createNeuralBackground() {
      const container = document.getElementById('neural-bg');
      if (!container) return;
      
      // Create particles
      for (let i = 0; i < 50; i++) {
        const particle = document.createElement('div');
        particle.className = 'neural-particle';
        particle.style.left = Math.random() * 100 + '%';
        particle.style.top = Math.random() * 100 + '%';
        particle.style.animationDelay = Math.random() * 20 + 's';
        particle.style.opacity = Math.random() * 0.3 + 0.1;
        container.appendChild(particle);
      }
      
      // Create connecting lines
      for (let i = 0; i < 20; i++) {
        const line = document.createElement('div');
        line.className = 'neural-line';
        line.style.left = Math.random() * 100 + '%';
        line.style.top = Math.random() * 100 + '%';
        line.style.width = Math.random() * 200 + 100 + 'px';
        line.style.transform = `rotate(${Math.random() * 360}deg)`;
        line.style.animationDelay = Math.random() * 8 + 's';
        container.appendChild(line);
      }
    }
    
    // Language toggle
    function toggleLanguage() {
      document.body.dir = document.body.dir === 'rtl' ? 'ltr' : 'rtl';
    }
    
    // Form handler
    function handleSignup(e) {
      e.preventDefault();
      const form = e.target;
      const email = form.querySelector('input[type="email"]').value;
      
      // Show success message
      const button = form.querySelector('button');
      const originalText = button.textContent;
      button.textContent = '✓ Welcome!';
      button.classList.add('bg-green-500');
      
      setTimeout(() => {
        button.textContent = originalText;
        button.classList.remove('bg-green-500');
        form.reset();
      }, 2000);
    }
    
    // Initialize
    createNeuralBackground();
    
    // Smooth scroll for anchor links
    document.querySelectorAll('a[href^="#"]').forEach(anchor => {
      anchor.addEventListener('click', function(e) {
        e.preventDefault();
        const target = document.querySelector(this.getAttribute('href'));
        if (target) {
          target.scrollIntoView({ behavior: 'smooth' });
        }
      });
    });
  </script>
 <script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9d72320337cbcfe8',t:'MTc3MjY0MTA5MS4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
