<!DOCTYPE html>
<html lang="en" class="h-full">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy Birthday Sri Lakshmi!</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome CDN -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@600;700;800;900&family=Great+Vibes&family=Montserrat:wght@300;400;500;600;700&family=Playfair+Display:ital,wght@0,400;0,600;1,400&display=swap" rel="stylesheet">
    <!-- Canvas Confetti CDN -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        roseGold: '#B76E79',
                        deepRose: '#4A0E17',
                        royalGold: '#D4AF37',
                        champagne: '#F7E7CE',
                        softPink: '#FFF0F3',
                    },
                    fontFamily: {
                        cinzel: ['Cinzel', 'serif'],
                        greatVibes: ['Great Vibes', 'cursive'],
                        playfair: ['Playfair Display', 'serif'],
                        sans: ['Montserrat', 'sans-serif'],
                    }
                }
            }
        }
    </script>

    <style>
        body {
            font-family: 'Montserrat', sans-serif;
            background: linear-gradient(135deg, #1a0509 0%, #2b0812 40%, #150307 70%, #0d0104 100%);
            color: #fce7f3;
            overflow-x: hidden;
            user-select: none;
        }

        .glass-card {
            background: rgba(45, 12, 22, 0.45);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid rgba(212, 175, 55, 0.25);
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.6), inset 0 0 15px rgba(212, 175, 55, 0.1);
        }

        .gold-gradient-text {
            background: linear-gradient(135deg, #FFE5A3 0%, #D4AF37 50%, #AA7C11 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .floating-heart {
            position: fixed;
            pointer-events: none;
            z-index: 1;
            animation: floatUp 8s linear infinite;
            opacity: 0.7;
        }

        @keyframes floatUp {
            0% {
                transform: translateY(105vh) scale(0.5) rotate(0deg);
                opacity: 0;
            }
            20% { opacity: 0.8; }
            80% { opacity: 0.8; }
            100% {
                transform: translateY(-10vh) scale(1.2) rotate(360deg);
                opacity: 0;
            }
        }

        .flame {
            width: 14px;
            height: 24px;
            background: radial-gradient(ellipse at bottom, #FFF 0%, #FFD700 25%, #FF4500 70%, transparent 100%);
            border-radius: 50% 50% 35% 35%;
            animation: flicker 0.15s infinite alternate ease-in-out;
            transform-origin: center bottom;
            box-shadow: 0 0 15px #FFD700, 0 0 25px #FF4500;
        }

        @keyframes flicker {
            0% { transform: scale(1) rotate(-2deg); }
            100% { transform: scale(1.15) rotate(2deg); opacity: 0.95; }
        }

        .smoke {
            position: absolute;
            width: 6px;
            height: 6px;
            background: rgba(200, 200, 200, 0.7);
            border-radius: 50%;
            animation: smokeRise 2s ease-out forwards;
            pointer-events: none;
        }

        @keyframes smokeRise {
            0% { opacity: 0.8; transform: translateY(0) scale(1); }
            100% { opacity: 0; transform: translateY(-40px) scale(3); filter: blur(4px); }
        }

        .cake-container {
            perspective: 1000px;
        }
        
        .top-surface-text {
            transform: rotateX(50deg) rotateZ(-5deg);
            font-family: 'Great Vibes', cursive;
            letter-spacing: 1.5px;
            text-shadow: 1px 1px 2px rgba(90, 10, 30, 0.8), 0 0 5px rgba(255, 255, 255, 0.9);
        }

        .gift-box {
            position: relative;
            transition: transform 0.5s ease;
            cursor: pointer;
        }

        .gift-lid {
            transition: transform 0.8s cubic-bezier(0.68, -0.55, 0.265, 1.55);
            transform-origin: top center;
        }

        .gift-box.open .gift-lid {
            transform: translateY(-80px) rotate(-15deg);
        }

        .page-section {
            display: none;
            opacity: 0;
            transition: opacity 0.6s ease-in-out, transform 0.6s ease-in-out;
            transform: translateY(15px);
        }

        .page-section.active {
            display: flex;
            opacity: 1;
            transform: translateY(0);
        }

        .glow-gold {
            box-shadow: 0 0 25px rgba(212, 175, 55, 0.4);
        }

        ::-webkit-scrollbar {
            width: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #1a0509;
        }
        ::-webkit-scrollbar-thumb {
            background: #D4AF37;
            border-radius: 3px;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col justify-between relative">

    <canvas id="particleCanvas" class="fixed inset-0 pointer-events-none z-0"></canvas>
    <canvas id="fireworksCanvas" class="fixed inset-0 pointer-events-none z-40"></canvas>

    <div id="floatingHeartsContainer" class="fixed inset-0 pointer-events-none z-0"></div>

    <audio id="bgAudio" loop preload="auto">
        <source src="https://raw.githubusercontent.com/krishnatejap76-arch/birtdaysurprise/d7c5117e5452b0195f9507b698e96a8d880b4e65/Happy%20Instrumental%20Background%20Music%20for%20Video%20and%20Presentations%20-%20Paradise%20City%20-%20Basspartout%20-%20Instrumental%20Background%20Music.mp3" type="audio/mp3">
    </audio>

    <header id="appHeader" class="hidden fixed top-0 left-0 right-0 z-50 px-6 py-4 flex justify-between items-center backdrop-blur-md bg-opacity-40 bg-black border-b border-yellow-500/20">
        <div class="flex items-center space-x-3">
            <span class="text-xl font-cinzel tracking-widest gold-gradient-text font-bold">SRI LAKSHMI</span>
            <span class="text-xs px-2.5 py-0.5 rounded-full bg-rose-900/60 text-pink-200 border border-pink-500/30">Birthday Edition</span>
        </div>
        
        <div class="flex items-center space-x-4">
            <button id="musicToggleBtn" onclick="toggleAudio()" class="w-10 h-10 rounded-full glass-card flex items-center justify-center text-yellow-400 hover:text-yellow-200 transition-all hover:scale-105 active:scale-95" title="Toggle Music">
                <i id="musicIcon" class="fas fa-music text-lg"></i>
            </button>
            
            <div class="glass-card px-3 py-1 rounded-full text-xs font-mono text-yellow-300 border border-yellow-500/30">
                Page <span id="currentPageNum">1</span> / 12
            </div>
        </div>
    </header>

    <main class="relative z-10 flex-grow flex items-center justify-center p-4 md:p-8 min-h-screen">

        <!-- PAGE 1: SECRET UNLOCKING GATE -->
        <section id="page1" class="page-section active flex-col items-center justify-center text-center max-w-xl w-full my-auto py-12">
            <div class="glass-card p-8 md:p-12 rounded-3xl w-full relative overflow-hidden border border-yellow-500/40 glow-gold">
                <div class="absolute -top-12 -right-12 w-32 h-32 bg-pink-500/20 rounded-full blur-2xl"></div>
                <div class="absolute -bottom-12 -left-12 w-32 h-32 bg-yellow-500/20 rounded-full blur-2xl"></div>
                
                <div class="mb-6 inline-block p-4 rounded-full bg-rose-950/60 border border-yellow-500/30 text-yellow-400 animate-bounce">
                    <i class="fas fa-lock text-3xl"></i>
                </div>

                <h1 class="font-cinzel text-2xl md:text-3xl font-bold tracking-wider mb-2 gold-gradient-text">
                    A SPECIAL SURPRISE AWAITS
                </h1>
                <p class="text-pink-200/80 text-sm md:text-base mb-8 font-light">
                    Enter the secret passkey to unlock the magical celebration created just for you.
                </p>

                <form onsubmit="handleSecretSubmit(event)" class="space-y-6">
                    <div class="relative">
                        <input type="password" id="secretInput" placeholder="Enter Secret Word..." 
                            class="w-full px-6 py-4 rounded-full bg-black/60 border-2 border-yellow-500/40 text-center text-lg text-yellow-200 placeholder-pink-300/40 focus:outline-none focus:border-yellow-400 transition-all font-mono shadow-inner"
                            autocomplete="off">
                        <p id="secretError" class="text-rose-400 text-xs mt-2 hidden animate-pulse">
                            <i class="fas fa-exclamation-circle mr-1"></i> Incorrect secret word! Hint: Passkey starts with 'M'
                        </p>
                    </div>

                    <button type="submit" 
                        class="w-full py-4 rounded-full bg-gradient-to-r from-yellow-600 via-amber-500 to-yellow-600 text-slate-950 font-bold font-cinzel text-lg tracking-widest shadow-lg hover:shadow-yellow-500/50 hover:scale-[1.02] active:scale-[0.98] transition-all duration-300 flex items-center justify-center space-x-2">
                        <span>UNLOCK SURPRISE</span>
                        <i class="fas fa-key"></i>
                    </button>
                </form>

                <p class="text-xs text-pink-300/40 mt-6 font-mono">
                    <i class="fas fa-heart text-pink-500 mr-1"></i> Designed exclusively for Sri Lakshmi
                </p>
            </div>
        </section>

        <!-- PAGE 2: GRAND WELCOME -->
        <section id="page2" class="page-section flex-col items-center justify-center text-center max-w-3xl w-full my-auto py-12">
            <div class="glass-card p-8 md:p-14 rounded-3xl w-full relative overflow-hidden text-center">
                <div class="text-pink-400 text-5xl mb-4 animate-pulse">
                    <i class="fas fa-crown"></i>
                </div>
                
                <h2 class="font-cinzel text-xl md:text-2xl text-yellow-300 tracking-widest uppercase mb-2">
                    Warmest Birthday Greetings
                </h2>
                
                <h1 class="font-greatVibes text-5xl md:text-7xl lg:text-8xl gold-gradient-text mb-6 py-2 leading-tight">
                    Happy Birthday Sri Lakshmi!
                </h1>
                
                <p class="text-pink-100 text-base md:text-xl font-playfair italic leading-relaxed mb-8 max-w-2xl mx-auto">
                    "May your day be filled with radiant joy, endless smiles, elegance, and moments as exceptionally beautiful as you are."
                </p>

                <div class="flex flex-wrap justify-center gap-4 text-xs font-mono text-yellow-200/80 mb-8">
                    <span class="px-4 py-2 rounded-full glass-card border border-yellow-500/20"><i class="fas fa-sparkles text-yellow-400 mr-1.5"></i>Elegance</span>
                    <span class="px-4 py-2 rounded-full glass-card border border-yellow-500/20"><i class="fas fa-star text-yellow-400 mr-1.5"></i>Grace</span>
                    <span class="px-4 py-2 rounded-full glass-card border border-yellow-500/20"><i class="fas fa-heart text-pink-400 mr-1.5"></i>Happiness</span>
                </div>

                <div class="pt-4">
                    <button onclick="nextPage()" class="px-8 py-3.5 rounded-full bg-gradient-to-r from-pink-600 to-rose-700 hover:from-pink-500 hover:to-rose-600 text-white font-semibold tracking-wider shadow-lg hover:shadow-pink-500/30 transition-all hover:scale-105 active:scale-95 inline-flex items-center space-x-3">
                        <span>Proceed to the Cake Ceremony</span>
                        <i class="fas fa-arrow-right"></i>
                    </button>
                </div>
            </div>
        </section>

        <!-- PAGE 3: LUXURY BIRTHDAY CAKE -->
        <section id="page3" class="page-section flex-col items-center justify-center text-center max-w-3xl w-full my-auto py-8">
            <div class="glass-card p-6 md:p-10 rounded-3xl w-full relative">
                <h2 class="font-cinzel text-2xl md:text-3xl font-bold gold-gradient-text mb-2">
                    LUXURY BIRTHDAY CAKE
                </h2>
                <p class="text-xs md:text-sm text-pink-200/80 mb-6">
                    <i class="fas fa-microphone text-yellow-400 mr-1"></i> Blow into your microphone or tap the candles below to extinguish them!
                </p>

                <div class="relative py-8 my-4 flex flex-col items-center justify-center min-h-[360px]">
                    <div class="cake-container relative flex flex-col items-center">
                        <div id="candlesRow" class="flex justify-center space-x-6 z-30 mb-[-10px]">
                            <div class="candle-item relative flex flex-col items-center cursor-pointer" onclick="extinguishCandle(this)">
                                <div class="flame shadow-lg"></div>
                                <div class="w-2.5 h-10 bg-gradient-to-b from-yellow-200 via-pink-300 to-yellow-100 rounded-sm border border-yellow-400/40"></div>
                            </div>
                            <div class="candle-item relative flex flex-col items-center cursor-pointer" onclick="extinguishCandle(this)">
                                <div class="flame shadow-lg"></div>
                                <div class="w-2.5 h-12 bg-gradient-to-b from-yellow-200 via-yellow-100 to-pink-300 rounded-sm border border-yellow-400/40"></div>
                            </div>
                            <div class="candle-item relative flex flex-col items-center cursor-pointer" onclick="extinguishCandle(this)">
                                <div class="flame shadow-lg"></div>
                                <div class="w-2.5 h-10 bg-gradient-to-b from-pink-300 via-yellow-200 to-yellow-100 rounded-sm border border-yellow-400/40"></div>
                            </div>
                        </div>

                        <!-- TIER 1 (TOP TIER WITH TEXT "HAPPY BIRTHDAY LUCKY") -->
                        <div class="relative w-48 h-24 bg-gradient-to-b from-pink-100 via-rose-200 to-pink-300 rounded-t-3xl border-2 border-yellow-400/60 shadow-xl flex flex-col items-center justify-start pt-2 overflow-visible z-20">
                            <div class="absolute -top-3 left-0 right-0 h-4 flex justify-around">
                                <div class="w-4 h-4 bg-white rounded-full shadow-inner border border-pink-200"></div>
                                <div class="w-4 h-4 bg-white rounded-full shadow-inner border border-pink-200"></div>
                                <div class="w-4 h-4 bg-white rounded-full shadow-inner border border-pink-200"></div>
                                <div class="w-4 h-4 bg-white rounded-full shadow-inner border border-pink-200"></div>
                                <div class="w-4 h-4 bg-white rounded-full shadow-inner border border-pink-200"></div>
                                <div class="w-4 h-4 bg-white rounded-full shadow-inner border border-pink-200"></div>
                            </div>
                            
                            <!-- TOP SURFACE TEXT -->
                            <div class="top-surface-text text-amber-950 font-bold text-sm text-center font-serif leading-tight mt-1 px-2 select-none">
                                Happy Birthday<br>
                                <span class="text-rose-900 font-extrabold text-base tracking-wider uppercase">LUCKY</span>
                            </div>

                            <div class="absolute bottom-1 left-2 right-2 flex justify-between">
                                <span class="w-2 h-2 rounded-full bg-yellow-300 shadow"></span>
                                <span class="w-2 h-2 rounded-full bg-pink-400 shadow"></span>
                                <span class="w-2 h-2 rounded-full bg-yellow-300 shadow"></span>
                                <span class="w-2 h-2 rounded-full bg-pink-400 shadow"></span>
                                <span class="w-2 h-2 rounded-full bg-yellow-300 shadow"></span>
                            </div>
                        </div>

                        <!-- TIER 2 -->
                        <div class="relative w-64 h-24 bg-gradient-to-b from-rose-200 via-pink-300 to-rose-400 rounded-t-xl border-2 border-yellow-400/60 shadow-xl flex items-center justify-center z-10 -mt-2">
                            <div class="w-full h-3 bg-gradient-to-r from-yellow-500 via-amber-300 to-yellow-500 my-auto shadow-inner flex justify-around items-center">
                                <div class="w-2 h-2 rounded-full bg-white shadow-sm"></div>
                                <div class="w-2 h-2 rounded-full bg-white shadow-sm"></div>
                                <div class="w-2 h-2 rounded-full bg-white shadow-sm"></div>
                                <div class="w-2 h-2 rounded-full bg-white shadow-sm"></div>
                            </div>
                            <div class="absolute right-4 top-2 text-rose-600 text-lg">
                                <i class="fas fa-spa"></i>
                            </div>
                            <div class="absolute left-4 top-2 text-rose-600 text-lg">
                                <i class="fas fa-spa"></i>
                            </div>
                        </div>

                        <!-- TIER 3 -->
                        <div class="relative w-80 h-24 bg-gradient-to-b from-pink-300 via-rose-300 to-rose-500 rounded-t-xl border-2 border-yellow-400/70 shadow-2xl flex items-center justify-center -mt-2 z-0">
                            <div class="w-full flex justify-center space-x-3 text-yellow-200 text-xs opacity-90">
                                <span>✦</span><span>✧</span><span>✦</span><span>✧</span><span>✦</span><span>✧</span><span>✦</span>
                            </div>
                            <div class="absolute -left-3 bottom-2 text-yellow-300 text-2xl drop-shadow">
                                <i class="fas fa-seedling"></i>
                            </div>
                            <div class="absolute -right-3 bottom-2 text-yellow-300 text-2xl drop-shadow">
                                <i class="fas fa-seedling"></i>
                            </div>
                        </div>

                        <div class="w-96 h-6 bg-gradient-to-r from-amber-200 via-yellow-400 to-amber-200 rounded-full border-2 border-yellow-600 shadow-2xl -mt-1 z-0"></div>
                        <div class="w-48 h-8 bg-gradient-to-b from-yellow-500 to-amber-700 rounded-b-xl shadow-2xl z-0"></div>
                    </div>
                </div>

                <div class="mt-4 flex flex-wrap justify-center gap-4">
                    <button id="blowCandlesBtn" onclick="blowAllCandles()" 
                        class="px-6 py-3 rounded-full bg-gradient-to-r from-yellow-500 to-amber-600 hover:from-yellow-400 hover:to-amber-500 text-slate-950 font-bold font-cinzel text-sm tracking-widest shadow-lg hover:scale-105 active:scale-95 transition-all">
                        <i class="fas fa-wind mr-2"></i> BLOW OUT CANDLES
                    </button>
                    <button id="micPermissionBtn" onclick="initMicDetection()" 
                        class="px-6 py-3 rounded-full glass-card border border-yellow-500/40 text-yellow-300 text-xs font-mono hover:bg-yellow-500/10 transition-all">
                        <i class="fas fa-microphone mr-2"></i> Enable Mic Blow Detection
                    </button>
                </div>

                <div id="cakeNextNav" class="mt-8 hidden">
                    <button onclick="nextPage()" class="px-8 py-3.5 rounded-full bg-gradient-to-r from-pink-600 to-rose-700 hover:from-pink-500 hover:to-rose-600 text-white font-semibold tracking-wider shadow-lg hover:shadow-pink-500/30 transition-all hover:scale-105 active:scale-95 inline-flex items-center space-x-3 animate-pulse">
                        <span>Explore Photo Showcase</span>
                        <i class="fas fa-arrow-right"></i>
                    </button>
                </div>
            </div>
        </section>

        <!-- PAGE 4: PHOTO SHOWCASE 1 -->
        <section id="page4" class="page-section flex-col items-center justify-center max-w-4xl w-full my-auto py-8">
            <div class="glass-card p-6 md:p-10 rounded-3xl w-full">
                <div class="text-center mb-6">
                    <span class="text-xs font-mono text-yellow-400 uppercase tracking-widest">Solo Gallery 01</span>
                    <h2 class="font-cinzel text-2xl md:text-4xl font-bold gold-gradient-text mt-1">A Collection of Beautiful Clicks</h2>
                </div>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6 items-center">
                    <div class="glass-card p-3 rounded-2xl overflow-hidden border border-pink-500/30 hover:border-yellow-400/60 transition-all duration-500 group">
                        <div class="aspect-[3/4] overflow-hidden rounded-xl relative">
                            <img src="https://raw.githubusercontent.com/krishnatejap76-arch/birtdaysurprise/d7c5117e5452b0195f9507b698e96a8d880b4e65/image%201.jpeg" 
                                alt="Sri Lakshmi Click 1" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-700">
                        </div>
                        <p class="text-center text-sm font-playfair italic text-pink-200 mt-3">"Some pictures don't need filters to shine."</p>
                    </div>
                    <div class="glass-card p-3 rounded-2xl overflow-hidden border border-pink-500/30 hover:border-yellow-400/60 transition-all duration-500 group">
                        <div class="aspect-[3/4] overflow-hidden rounded-xl relative">
                            <img src="https://raw.githubusercontent.com/krishnatejap76-arch/birtdaysurprise/d7c5117e5452b0195f9507b698e96a8d880b4e65/image%202.jpeg" 
                                alt="Sri Lakshmi Click 2" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-700">
                        </div>
                        <p class="text-center text-sm font-playfair italic text-pink-200 mt-3">"A beautiful click deserves a beautiful frame."</p>
                    </div>
                </div>
                <div class="mt-8 flex justify-between items-center">
                    <button onclick="prevPage()" class="px-5 py-2.5 rounded-full glass-card border border-yellow-500/30 text-yellow-300 text-xs hover:bg-yellow-500/10">
                        <i class="fas fa-arrow-left mr-2"></i> Previous
                    </button>
                    <button onclick="nextPage()" class="px-6 py-2.5 rounded-full bg-gradient-to-r from-pink-600 to-rose-700 text-white text-xs font-semibold tracking-wider hover:scale-105 transition-all">
                        Next Surprise <i class="fas fa-arrow-right ml-2"></i>
                    </button>
                </div>
            </div>
        </section>

        <!-- PAGE 5: PHOTO SHOWCASE 2 -->
        <section id="page5" class="page-section flex-col items-center justify-center max-w-4xl w-full my-auto py-8">
            <div class="glass-card p-6 md:p-10 rounded-3xl w-full">
                <div class="text-center mb-6">
                    <span class="text-xs font-mono text-yellow-400 uppercase tracking-widest">Solo Gallery 02</span>
                    <h2 class="font-cinzel text-2xl md:text-4xl font-bold gold-gradient-text mt-1">Every Picture Has Its Own Magic</h2>
                </div>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6 items-center">
                    <div class="glass-card p-3 rounded-2xl overflow-hidden border border-pink-500/30 hover:border-yellow-400/60 transition-all duration-500 group">
                        <div class="aspect-[3/4] overflow-hidden rounded-xl relative">
                            <img src="https://raw.githubusercontent.com/krishnatejap76-arch/birtdaysurprise/d7c5117e5452b0195f9507b698e96a8d880b4e65/image%203.jpeg" 
                                alt="Sri Lakshmi Click 3" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-700">
                        </div>
                        <p class="text-center text-sm font-playfair italic text-pink-200 mt-3">"Every picture tells its own little story."</p>
                    </div>
                    <div class="glass-card p-3 rounded-2xl overflow-hidden border border-pink-500/30 hover:border-yellow-400/60 transition-all duration-500 group">
                        <div class="aspect-[3/4] overflow-hidden rounded-xl relative">
                            <img src="https://raw.githubusercontent.com/krishnatejap76-arch/birtdaysurprise/d7c5117e5452b0195f9507b698e96a8d880b4e65/image%204.jpeg" 
                                alt="Sri Lakshmi Click 4" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-700">
                        </div>
                        <p class="text-center text-sm font-playfair italic text-pink-200 mt-3">"That smile makes the moment special."</p>
                    </div>
                </div>
                <div class="mt-8 flex justify-between items-center">
                    <button onclick="prevPage()" class="px-5 py-2.5 rounded-full glass-card border border-yellow-500/30 text-yellow-300 text-xs hover:bg-yellow-500/10">
                        <i class="fas fa-arrow-left mr-2"></i> Previous
                    </button>
                    <button onclick="nextPage()" class="px-6 py-2.5 rounded-full bg-gradient-to-r from-pink-600 to-rose-700 text-white text-xs font-semibold tracking-wider hover:scale-105 transition-all">
                        Next Surprise <i class="fas fa-arrow-right ml-2"></i>
                    </button>
                </div>
            </div>
        </section>

        <!-- PAGE 6: PHOTO SHOWCASE 3 -->
        <section id="page6" class="page-section flex-col items-center justify-center max-w-4xl w-full my-auto py-8">
            <div class="glass-card p-6 md:p-10 rounded-3xl w-full">
                <div class="text-center mb-6">
                    <span class="text-xs font-mono text-yellow-400 uppercase tracking-widest">Solo Gallery 03</span>
                    <h2 class="font-cinzel text-2xl md:text-4xl font-bold gold-gradient-text mt-1">Elegance in Every Frame</h2>
                </div>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6 items-center">
                    <div class="glass-card p-3 rounded-2xl overflow-hidden border border-pink-500/30 hover:border-yellow-400/60 transition-all duration-500 group">
                        <div class="aspect-[3/4] overflow-hidden rounded-xl relative">
                            <img src="https://raw.githubusercontent.com/krishnatejap76-arch/birtdaysurprise/d7c5117e5452b0195f9507b698e96a8d880b4e65/image%205.jpeg" 
                                alt="Sri Lakshmi Click 5" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-700">
                        </div>
                        <p class="text-center text-sm font-playfair italic text-pink-200 mt-3">"Elegance captured in a single frame."</p>
                    </div>
                    <div class="glass-card p-3 rounded-2xl overflow-hidden border border-pink-500/30 hover:border-yellow-400/60 transition-all duration-500 group">
                        <div class="aspect-[3/4] overflow-hidden rounded-xl relative">
                            <img src="https://raw.githubusercontent.com/krishnatejap76-arch/birtdaysurprise/d7c5117e5452b0195f9507b698e96a8d880b4e65/image%206.jpeg" 
                                alt="Sri Lakshmi Click 6" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-700">
                        </div>
                        <p class="text-center text-sm font-playfair italic text-pink-200 mt-3">"A little sparkle in every picture."</p>
                    </div>
                </div>
                <div class="mt-8 flex justify-between items-center">
                    <button onclick="prevPage()" class="px-5 py-2.5 rounded-full glass-card border border-yellow-500/30 text-yellow-300 text-xs hover:bg-yellow-500/10">
                        <i class="fas fa-arrow-left mr-2"></i> Previous
                    </button>
                    <button onclick="nextPage()" class="px-6 py-2.5 rounded-full bg-gradient-to-r from-pink-600 to-rose-700 text-white text-xs font-semibold tracking-wider hover:scale-105 transition-all">
                        Next Surprise <i class="fas fa-arrow-right ml-2"></i>
                    </button>
                </div>
            </div>
        </section>

        <!-- PAGE 7: PHOTO SHOWCASE 4 -->
        <section id="page7" class="page-section flex-col items-center justify-center max-w-4xl w-full my-auto py-8">
            <div class="glass-card p-6 md:p-10 rounded-3xl w-full">
                <div class="text-center mb-6">
                    <span class="text-xs font-mono text-yellow-400 uppercase tracking-widest">Solo Gallery 04</span>
                    <h2 class="font-cinzel text-2xl md:text-4xl font-bold gold-gradient-text mt-1">A Gallery of Beautiful Moments</h2>
                </div>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6 items-center">
                    <div class="glass-card p-3 rounded-2xl overflow-hidden border border-pink-500/30 hover:border-yellow-400/60 transition-all duration-500 group">
                        <div class="aspect-[3/4] overflow-hidden rounded-xl relative">
                            <img src="https://raw.githubusercontent.com/krishnatejap76-arch/birtdaysurprise/d7c5117e5452b0195f9507b698e96a8d880b4e65/image%207.jpeg" 
                                alt="Sri Lakshmi Click 7" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-700">
                        </div>
                        <p class="text-center text-sm font-playfair italic text-pink-200 mt-3">"Some clicks are simply unforgettable."</p>
                    </div>
                    <div class="glass-card p-3 rounded-2xl overflow-hidden border border-pink-500/30 hover:border-yellow-400/60 transition-all duration-500 group">
                        <div class="aspect-[3/4] overflow-hidden rounded-xl relative">
                            <img src="https://raw.githubusercontent.com/krishnatejap76-arch/birtdaysurprise/d7c5117e5452b0195f9507b698e96a8d880b4e65/image%208.jpeg" 
                                alt="Sri Lakshmi Click 8" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-700">
                        </div>
                        <p class="text-center text-sm font-playfair italic text-pink-200 mt-3">"Pure simplicity and poise."</p>
                    </div>
                </div>
                <div class="mt-8 flex justify-between items-center">
                    <button onclick="prevPage()" class="px-5 py-2.5 rounded-full glass-card border border-yellow-500/30 text-yellow-300 text-xs hover:bg-yellow-500/10">
                        <i class="fas fa-arrow-left mr-2"></i> Previous
                    </button>
                    <button onclick="nextPage()" class="px-6 py-2.5 rounded-full bg-gradient-to-r from-pink-600 to-rose-700 text-white text-xs font-semibold tracking-wider hover:scale-105 transition-all">
                        Next Surprise <i class="fas fa-arrow-right ml-2"></i>
                    </button>
                </div>
            </div>
        </section>

        <!-- PAGE 8: PHOTO SHOWCASE 5 -->
        <section id="page8" class="page-section flex-col items-center justify-center max-w-4xl w-full my-auto py-8">
            <div class="glass-card p-6 md:p-10 rounded-3xl w-full">
                <div class="text-center mb-6">
                    <span class="text-xs font-mono text-yellow-400 uppercase tracking-widest">Solo Gallery 05</span>
                    <h2 class="font-cinzel text-2xl md:text-4xl font-bold gold-gradient-text mt-1">Beauty Beyond Words</h2>
                </div>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6 items-center">
                    <div class="glass-card p-3 rounded-2xl overflow-hidden border border-pink-500/30 hover:border-yellow-400/60 transition-all duration-500 group">
                        <div class="aspect-[3/4] overflow-hidden rounded-xl relative">
                            <img src="https://raw.githubusercontent.com/krishnatejap76-arch/birtdaysurprise/d7c5117e5452b0195f9507b698e96a8d880b4e65/image%209.jpeg" 
                                alt="Sri Lakshmi Click 9" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-700">
                        </div>
                        <p class="text-center text-sm font-playfair italic text-pink-200 mt-3">"Radiating charm effortlessly."</p>
                    </div>
                    <div class="glass-card p-3 rounded-2xl overflow-hidden border border-pink-500/30 hover:border-yellow-400/60 transition-all duration-500 group">
                        <div class="aspect-[3/4] overflow-hidden rounded-xl relative">
                            <img src="https://raw.githubusercontent.com/krishnatejap76-arch/birtdaysurprise/d7c5117e5452b0195f9507b698e96a8d880b4e65/image%2010.jpeg" 
                                alt="Sri Lakshmi Click 10" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-700">
                        </div>
                        <p class="text-center text-sm font-playfair italic text-pink-200 mt-3">"A timeless portrait of grace."</p>
                    </div>
                </div>
                <div class="mt-8 flex justify-between items-center">
                    <button onclick="prevPage()" class="px-5 py-2.5 rounded-full glass-card border border-yellow-500/30 text-yellow-300 text-xs hover:bg-yellow-500/10">
                        <i class="fas fa-arrow-left mr-2"></i> Previous
                    </button>
                    <button onclick="nextPage()" class="px-6 py-2.5 rounded-full bg-gradient-to-r from-pink-600 to-rose-700 text-white text-xs font-semibold tracking-wider hover:scale-105 transition-all">
                        Next Surprise <i class="fas fa-arrow-right ml-2"></i>
                    </button>
                </div>
            </div>
        </section>

        <!-- PAGE 9: PHOTO SHOWCASE 6 -->
        <section id="page9" class="page-section flex-col items-center justify-center max-w-4xl w-full my-auto py-8">
            <div class="glass-card p-6 md:p-10 rounded-3xl w-full">
                <div class="text-center mb-6">
                    <span class="text-xs font-mono text-yellow-400 uppercase tracking-widest">Solo Gallery 06</span>
                    <h2 class="font-cinzel text-2xl md:text-4xl font-bold gold-gradient-text mt-1">The Art of Being Beautiful</h2>
                </div>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6 items-center">
                    <div class="glass-card p-3 rounded-2xl overflow-hidden border border-pink-500/30 hover:border-yellow-400/60 transition-all duration-500 group">
                        <div class="aspect-[3/4] overflow-hidden rounded-xl relative">
                            <img src="https://raw.githubusercontent.com/krishnatejap76-arch/birtdaysurprise/d7c5117e5452b0195f9507b698e96a8d880b4e65/image%2011.jpeg" 
                                alt="Sri Lakshmi Click 11" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-700">
                        </div>
                        <p class="text-center text-sm font-playfair italic text-pink-200 mt-3">"A little collection of happiness."</p>
                    </div>
                    <div class="glass-card p-3 rounded-2xl overflow-hidden border border-pink-500/30 hover:border-yellow-400/60 transition-all duration-500 group">
                        <div class="aspect-[3/4] overflow-hidden rounded-xl relative">
                            <img src="https://raw.githubusercontent.com/krishnatejap76-arch/birtdaysurprise/d7c5117e5452b0195f9507b698e96a8d880b4e65/image%2012.jpeg" 
                                alt="Sri Lakshmi Click 12" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-700">
                        </div>
                        <p class="text-center text-sm font-playfair italic text-pink-200 mt-3">"Her beautiful world in full highlight."</p>
                    </div>
                </div>
                <div class="mt-8 flex justify-between items-center">
                    <button onclick="prevPage()" class="px-5 py-2.5 rounded-full glass-card border border-yellow-500/30 text-yellow-300 text-xs hover:bg-yellow-500/10">
                        <i class="fas fa-arrow-left mr-2"></i> Previous
                    </button>
                    <button onclick="nextPage()" class="px-6 py-2.5 rounded-full bg-gradient-to-r from-pink-600 to-rose-700 text-white text-xs font-semibold tracking-wider hover:scale-105 transition-all">
                        Unwrap Gift <i class="fas fa-gift ml-2"></i>
                    </button>
                </div>
            </div>
        </section>

        <!-- PAGE 10: INTERACTIVE GIFT BOX & LETTER -->
        <section id="page10" class="page-section flex-col items-center justify-center text-center max-w-2xl w-full my-auto py-8">
            <div class="glass-card p-6 md:p-10 rounded-3xl w-full relative flex flex-col items-center">
                <h2 class="font-cinzel text-2xl md:text-3xl font-bold gold-gradient-text mb-2">
                    A SPECIAL SURPRISE GIFT
                </h2>
                <p class="text-xs text-pink-200/80 mb-6 font-mono">Tap the luxury gift box below to open!</p>

                <div id="giftBoxContainer" class="gift-box my-6" onclick="openGiftBox()">
                    <div class="gift-lid w-40 h-10 bg-gradient-to-r from-rose-600 via-pink-500 to-rose-600 rounded-t-lg border-b-2 border-yellow-400 shadow-xl relative z-10 flex justify-center items-center">
                        <div class="w-8 h-full bg-yellow-400"></div>
                        <div class="absolute -top-6 w-12 h-6 flex justify-center items-center">
                            <div class="w-6 h-6 rounded-full border-4 border-yellow-400 bg-transparent rotate-45"></div>
                            <div class="w-6 h-6 rounded-full border-4 border-yellow-400 bg-transparent -rotate-45 -ml-2"></div>
                        </div>
                    </div>
                    <div class="w-36 h-36 bg-gradient-to-b from-rose-700 to-rose-900 rounded-b-lg border-2 border-yellow-500/50 shadow-2xl relative flex justify-center overflow-hidden">
                        <div class="w-8 h-full bg-yellow-400 shadow-md"></div>
                        <div class="absolute inset-0 flex items-center justify-center text-yellow-300 text-xl font-bold opacity-30">
                            ✦
                        </div>
                    </div>
                </div>

                <div id="letterModal" class="hidden w-full mt-6 bg-pink-950/80 border border-yellow-500/40 rounded-2xl p-6 text-left shadow-2xl">
                    <div class="flex justify-between items-center mb-4 border-b border-yellow-500/20 pb-2">
                        <span class="font-cinzel text-yellow-300 text-sm font-bold">Special Letter for Sri Lakshmi</span>
                        <i class="fas fa-envelope-open-text text-pink-400 text-xl"></i>
                    </div>
                    <div class="font-playfair text-pink-100 text-sm md:text-base leading-relaxed space-y-4">
                        <p class="font-semibold text-yellow-200">Dearest Sri Lakshmi,</p>
                        <p>
                            On your special birthday, this gesture comes with warmth and wishes for your continued happiness, grace, and success. 
                            May this new chapter bring you endless reasons to smile, beautiful moments to cherish, and all the success you truly deserve.
                        </p>
                        <p>
                            Keep shining brightly with elegance and confidence!
                        </p>
                        <p class="text-right font-greatVibes text-2xl text-yellow-300 pt-2">
                            Happy Birthday! ✨
                        </p>
                    </div>
                </div>

                <div class="mt-8 flex justify-between items-center w-full">
                    <button onclick="prevPage()" class="px-5 py-2.5 rounded-full glass-card border border-yellow-500/30 text-yellow-300 text-xs hover:bg-yellow-500/10">
                        <i class="fas fa-arrow-left mr-2"></i> Previous
                    </button>
                    <button onclick="nextPage()" class="px-6 py-2.5 rounded-full bg-gradient-to-r from-pink-600 to-rose-700 text-white text-xs font-semibold tracking-wider hover:scale-105 transition-all">
                        Wait, One Last Click! 😜 <i class="fas fa-arrow-right ml-2"></i>
                    </button>
                </div>
            </div>
        </section>

        <!-- PAGE 11: EXTRA ANNOYING / PLAYFUL FINAL PHOTO PAGE -->
        <section id="page11" class="page-section flex-col items-center justify-center max-w-3xl w-full my-auto py-8">
            <div class="glass-card p-6 md:p-10 rounded-3xl w-full text-center">
                <div class="mb-4">
                    <span class="text-xs font-mono text-yellow-400 uppercase tracking-widest">Bonus Moment 🤪</span>
                    <h2 class="font-cinzel text-2xl md:text-4xl font-bold gold-gradient-text mt-1">The Unforgettable Final Click!</h2>
                </div>
                
                <div class="glass-card p-4 rounded-2xl overflow-hidden border border-yellow-500/40 hover:border-yellow-400/80 transition-all duration-500 max-w-md mx-auto my-4 group shadow-2xl">
                    <div class="aspect-[3/4] overflow-hidden rounded-xl relative">
                        <img src="https://raw.githubusercontent.com/krishnatejap76-arch/birtdaysurprise/ca187d9cad31b5540593432be898d3643fd16166/WhatsApp%20Image%202026-11-01%20at%207.05.51%20PM.jpeg" 
                            alt="Sri Lakshmi Special Click" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-700">
                    </div>
                    <p class="text-center text-sm font-playfair italic text-pink-200 mt-4">
                        "No birthday celebration is complete without this legendary click!"
                    </p>
                </div>

                <div class="mt-8 flex justify-between items-center">
                    <button onclick="prevPage()" class="px-5 py-2.5 rounded-full glass-card border border-yellow-500/30 text-yellow-300 text-xs hover:bg-yellow-500/10">
                        <i class="fas fa-arrow-left mr-2"></i> Previous
                    </button>
                    <button onclick="nextPage()" class="px-6 py-2.5 rounded-full bg-gradient-to-r from-pink-600 to-rose-700 text-white text-xs font-semibold tracking-wider hover:scale-105 transition-all">
                        Grand Finale <i class="fas fa-star ml-2"></i>
                    </button>
                </div>
            </div>
        </section>

        <!-- PAGE 12: GRAND FINALE -->
        <section id="page12" class="page-section flex-col items-center justify-center text-center max-w-3xl w-full my-auto py-8">
            <div class="glass-card p-8 md:p-12 rounded-3xl w-full relative text-center">
                <div class="inline-block p-4 rounded-full bg-yellow-500/10 text-yellow-400 mb-4 animate-bounce">
                    <i class="fas fa-glass-cheers text-4xl"></i>
                </div>

                <h1 class="font-cinzel text-3xl md:text-5xl font-bold gold-gradient-text mb-4">
                    CELEBRATING SRI LAKSHMI!
                </h1>

                <p class="text-pink-100 font-playfair text-base md:text-xl mb-8">
                    "Wishing you a year filled with sparkling moments, boundless happiness, and wonderful discoveries."
                </p>

                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 max-w-md mx-auto mb-8">
                    <button onclick="triggerGrandFireworks()" class="p-4 rounded-2xl glass-card border border-yellow-500/40 text-yellow-300 font-mono text-xs hover:bg-yellow-500/20 transition-all flex items-center justify-center space-x-2">
                        <i class="fas fa-fireworks text-base"></i>
                        <span>Launch Fireworks</span>
                    </button>
                    <button onclick="goToPage(1)" class="p-4 rounded-2xl glass-card border border-pink-500/40 text-pink-300 font-mono text-xs hover:bg-pink-500/20 transition-all flex items-center justify-center space-x-2">
                        <i class="fas fa-redo text-base"></i>
                        <span>Replay Surprise</span>
                    </button>
                </div>

                <div class="border-t border-yellow-500/20 pt-6">
                    <p class="text-xs text-pink-300/60 font-mono">
                        Happy Birthday Sri Lakshmi • Designed with Care & Best Wishes
                    </p>
                </div>
            </div>
        </section>

    </main>

    <footer id="appFooter" class="hidden fixed bottom-0 left-0 right-0 z-40 px-6 py-3 flex justify-between items-center backdrop-blur-md bg-black/40 border-t border-yellow-500/20 text-xs text-pink-200">
        <button onclick="prevPage()" class="hover:text-yellow-300 transition-colors flex items-center space-x-1">
            <i class="fas fa-chevron-left"></i><span>Back</span>
        </button>
        <span class="font-cinzel text-yellow-400/80 tracking-widest hidden sm:inline">SRI LAKSHMI BIRTHDAY SURPRISE</span>
        <button onclick="nextPage()" class="hover:text-yellow-300 transition-colors flex items-center space-x-1">
            <span>Next</span><i class="fas fa-chevron-right"></i>
        </button>
    </footer>

    <script>
        let currentPage = 1;
        const totalPages = 12;
        const secretWord = "manchidi";
        let isUnlocked = false;
        let remainingCandles = 3;

        const bgCanvas = document.getElementById('particleCanvas');
        const bgCtx = bgCanvas.getContext('2d');
        let bgParticles = [];

        function resizeCanvas() {
            bgCanvas.width = window.innerWidth;
            bgCanvas.height = window.innerHeight;
            const fwCanvas = document.getElementById('fireworksCanvas');
            if (fwCanvas) {
                fwCanvas.width = window.innerWidth;
                fwCanvas.height = window.innerHeight;
            }
        }
        window.addEventListener('resize', resizeCanvas);
        resizeCanvas();

        class Particle {
            constructor() {
                this.x = Math.random() * bgCanvas.width;
                this.y = Math.random() * bgCanvas.height;
                this.size = Math.random() * 2.5 + 0.5;
                this.speedY = Math.random() * 0.5 + 0.2;
                this.color = Math.random() > 0.5 ? 'rgba(212, 175, 55, ' : 'rgba(255, 182, 193, ';
                this.opacity = Math.random() * 0.6 + 0.2;
            }
            update() {
                this.y -= this.speedY;
                if (this.y < 0) {
                    this.y = bgCanvas.height;
                    this.x = Math.random() * bgCanvas.width;
                }
            }
            draw() {
                bgCtx.fillStyle = this.color + this.opacity + ')';
                bgCtx.beginPath();
                bgCtx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                bgCtx.fill();
            }
        }

        for (let i = 0; i < 70; i++) {
            bgParticles.push(new Particle());
        }

        function animateBgParticles() {
            bgCtx.clearRect(0, 0, bgCanvas.width, bgCanvas.height);
            bgParticles.forEach(p => {
                p.update();
                p.draw();
            });
            requestAnimationFrame(animateBgParticles);
        }
        animateBgParticles();

        function generateFloatingHearts() {
            const container = document.getElementById('floatingHeartsContainer');
            const heartIcons = ['❤️', '💖', '✨', '🌸', '✨'];
            setInterval(() => {
                if (!isUnlocked) return;
                const heart = document.createElement('div');
                heart.className = 'floating-heart text-sm md:text-lg';
                heart.innerText = heartIcons[Math.floor(Math.random() * heartIcons.length)];
                heart.style.left = Math.random() * 95 + 'vw';
                heart.style.animationDuration = (Math.random() * 4 + 6) + 's';
                container.appendChild(heart);
                setTimeout(() => heart.remove(), 10000);
            }, 1200);
        }

        function handleSecretSubmit(e) {
            e.preventDefault();
            const inputVal = document.getElementById('secretInput').value.trim().toLowerCase();
            const errElem = document.getElementById('secretError');

            if (inputVal === secretWord) {
                isUnlocked = true;
                errElem.classList.add('hidden');
                
                document.getElementById('appHeader').classList.remove('hidden');
                document.getElementById('appFooter').classList.remove('hidden');
                
                playBackgroundAudio();
                generateFloatingHearts();
                
                confetti({
                    particleCount: 80,
                    spread: 70,
                    origin: { y: 0.6 }
                });

                goToPage(2);
            } else {
                errElem.classList.remove('hidden');
            }
        }

        function playBackgroundAudio() {
            const audio = document.getElementById('bgAudio');
            audio.volume = 0.55;
            audio.play().catch(err => console.log("Audio autoplay restricted. User interaction allowed audio."));
        }

        function toggleAudio() {
            const audio = document.getElementById('bgAudio');
            const icon = document.getElementById('musicIcon');
            if (audio.paused) {
                audio.play();
                icon.className = 'fas fa-music text-lg';
            } else {
                audio.pause();
                icon.className = 'fas fa-volume-mute text-lg text-rose-400';
            }
        }

        function playBlastSound() {
            try {
                const ctx = new (window.AudioContext || window.webkitAudioContext)();
                const bufferSize = ctx.sampleRate * 0.4;
                const buffer = ctx.createBuffer(1, bufferSize, ctx.sampleRate);
                const output = buffer.getChannelData(0);
                for (let i = 0; i < bufferSize; i++) {
                    output[i] = Math.random() * 2 - 1;
                }

                const whiteNoise = ctx.createBufferSource();
                whiteNoise.buffer = buffer;

                const filter = ctx.createBiquadFilter();
                filter.type = 'lowpass';
                filter.frequency.setValueAtTime(1000, ctx.currentTime);
                filter.frequency.exponentialRampToValueAtTime(80, ctx.currentTime + 0.3);

                const gainNode = ctx.createGain();
                gainNode.gain.setValueAtTime(1, ctx.currentTime);
                gainNode.gain.exponentialRampToValueAtTime(0.01, ctx.currentTime + 0.35);

                whiteNoise.connect(filter);
                filter.connect(gainNode);
                gainNode.connect(ctx.destination);

                whiteNoise.start();
                whiteNoise.stop(ctx.currentTime + 0.4);
            } catch(e) {
                console.log("Audio synthesis error", e);
            }
        }

        function extinguishCandle(candleElem) {
            const flame = candleElem.querySelector('.flame');
            if (flame && flame.style.display !== 'none') {
                flame.style.display = 'none';
                
                const smoke = document.createElement('div');
                smoke.className = 'smoke';
                smoke.style.top = '-10px';
                candleElem.appendChild(smoke);
                
                remainingCandles--;

                if (remainingCandles <= 0) {
                    onAllCandlesBlown();
                }
            }
        }

        function blowAllCandles() {
            const candleItems = document.querySelectorAll('.candle-item');
            candleItems.forEach(item => extinguishCandle(item));
        }

        function onAllCandlesBlown() {
            playBlastSound();

            confetti({
                particleCount: 150,
                spread: 100,
                origin: { y: 0.5 }
            });

            triggerGrandFireworks();

            document.getElementById('cakeNextNav').classList.remove('hidden');
        }

        async function initMicDetection() {
            const btn = document.getElementById('micPermissionBtn');
            try {
                const stream = await navigator.mediaDevices.getUserMedia({ audio: true, video: false });
                btn.innerHTML = `<i class="fas fa-check text-green-400 mr-2"></i> Mic Active - Blow Now!`;
                
                const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
                const analyser = audioCtx.createAnalyser();
                const microphone = audioCtx.createMediaStreamSource(stream);
                microphone.connect(analyser);
                analyser.fftSize = 256;

                const bufferLength = analyser.frequencyBinCount;
                const dataArray = new Uint8Array(bufferLength);

                function checkVolume() {
                    analyser.getByteFrequencyData(dataArray);
                    let sum = 0;
                    for (let i = 0; i < bufferLength; i++) {
                        sum += dataArray[i];
                    }
                    let average = sum / bufferLength;

                    if (average > 65) {
                        blowAllCandles();
                    } else if (remainingCandles > 0) {
                        requestAnimationFrame(checkVolume);
                    }
                }
                checkVolume();
            } catch (err) {
                btn.innerText = "Mic access unavailable (Use Blow Button)";
            }
        }

        function openGiftBox() {
            const box = document.getElementById('giftBoxContainer');
            const letter = document.getElementById('letterModal');
            if (!box.classList.contains('open')) {
                box.classList.add('open');
                playBlastSound();
                confetti({
                    particleCount: 100,
                    spread: 80,
                    origin: { y: 0.6 }
                });
                setTimeout(() => {
                    letter.classList.remove('hidden');
                }, 400);
            }
        }

        function triggerGrandFireworks() {
            const fwCanvas = document.getElementById('fireworksCanvas');
            const ctx = fwCanvas.getContext('2d');
            let particles = [];

            for (let i = 0; i < 80; i++) {
                particles.push({
                    x: fwCanvas.width / 2,
                    y: fwCanvas.height / 2,
                    dx: (Math.random() - 0.5) * 12,
                    dy: (Math.random() - 0.5) * 12,
                    color: `hsl(${Math.random() * 360}, 100%, 60%)`,
                    radius: Math.random() * 3 + 1,
                    alpha: 1,
                    decay: Math.random() * 0.02 + 0.015
                });
            }

            function renderFireworks() {
                ctx.clearRect(0, 0, fwCanvas.width, fwCanvas.height);
                let alive = false;
                particles.forEach(p => {
                    if (p.alpha > 0) {
                        alive = true;
                        p.x += p.dx;
                        p.y += p.dy;
                        p.alpha -= p.decay;
                        ctx.save();
                        ctx.globalAlpha = Math.max(0, p.alpha);
                        ctx.fillStyle = p.color;
                        ctx.beginPath();
                        ctx.arc(p.x, p.y, p.radius, 0, Math.PI * 2);
                        ctx.fill();
                        ctx.restore();
                    }
                });
                if (alive) {
                    requestAnimationFrame(renderFireworks);
                }
            }
            renderFireworks();
        }

        function goToPage(pageNumber) {
            if (pageNumber < 1 || pageNumber > totalPages) return;
            
            const currentElem = document.getElementById(`page${currentPage}`);
            if (currentElem) {
                currentElem.classList.remove('active');
            }

            currentPage = pageNumber;
            document.getElementById('currentPageNum').innerText = currentPage;

            const nextElem = document.getElementById(`page${currentPage}`);
            if (nextElem) {
                nextElem.classList.add('active');
            }

            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        function nextPage() {
            if (currentPage < totalPages) {
                goToPage(currentPage + 1);
            }
        }

        function prevPage() {
            if (currentPage > 1) {
                goToPage(currentPage - 1);
            }
        }

        document.addEventListener('keydown', (e) => {
            if (!isUnlocked) return;
            if (e.key === 'ArrowRight') nextPage();
            if (e.key === 'ArrowLeft') prevPage();
        });
    </script>
</body>
</html>
