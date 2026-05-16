<!DOCTYPE html>
<html lang="ar" dir="rtl" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ASWAD STORE | Define The Dark</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://unpkg.com/lucide@latest"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/ScrollTrigger.min.js"></script>
    <script src="https://cdn.jsdelivr.net/gh/studio-freight/lenis@1.0.19/bundled/lenis.min.js"></script>
    
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;700&family=Playfair+Display:ital,wght=1,400&display=swap" rel="stylesheet">

    <style>
        :root {
            --black: #000000;
            --white: #F5F5F5;
            --dark-gray: #111111;
            --light-gray: #B3B3B3;
        }

        body {
            background-color: var(--black);
            color: var(--white);
            font-family: 'Inter', sans-serif;
            overflow-x: hidden;
        }

        @media (pointer: fine) {
            body { cursor: none; }
            #custom-cursor, #cursor-follower { display: block; }
        }
        @media (pointer: coarse), (max-width: 768px) {
            body { cursor: auto !important; }
            #custom-cursor, #cursor-follower { display: none !important; pointer-events: none !important; }
        }

        .font-serif-italic { font-family: 'Playfair Display', serif; font-style: italic; }

        ::-webkit-scrollbar { width: 4px; }
        ::-webkit-scrollbar-track { background: #000; }
        ::-webkit-scrollbar-thumb { background: #333; border-radius: 10px; }

        .glass {
            background: rgba(0, 0, 0, 0.7);
            backdrop-filter: blur(15px);
            -webkit-backdrop-filter: blur(15px);
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }

        #custom-cursor {
            position: fixed;
            width: 10px;
            height: 10px;
            background: white;
            border-radius: 50%;
            pointer-events: none;
            z-index: 9999;
            mix-blend-mode: difference;
            transition: transform 0.2s ease-out;
            transform: translate(-50%, -50%);
            display: none;
        }

        #cursor-follower {
            position: fixed;
            width: 40px;
            height: 40px;
            border: 1px solid rgba(255,255,255,0.3);
            border-radius: 50%;
            pointer-events: none;
            z-index: 9998;
            transition: transform 0.1s ease-out;
            transform: translate(-50%, -50%);
            display: none;
        }

        .product-image-container:hover .image-primary { opacity: 0; }
        .product-image-container:hover .image-secondary { opacity: 1; transform: scale(1.03); }

        .image-primary { transition: opacity 0.6s cubic-bezier(0.25, 1, 0.5, 1); }
        .image-secondary {
            opacity: 0;
            transition: all 0.6s cubic-bezier(0.25, 1, 0.5, 1);
        }

        .reveal-up { opacity: 0; transform: translateY(30px); }

        button, a, .cursor-pointer {
            transition: transform 0.2s cubic-bezier(0.25, 1, 0.5, 1);
        }
        button:active, a:active, .cursor-pointer:active {
            transform: scale(0.95) !important;
        }

        .size-btn.active {
            background-color: #FFFFFF !important;
            color: #000000 !important;
            border-color: #FFFFFF !important;
        }
    </style>
</head>
<body>

    <div id="custom-cursor"></div>
    <div id="cursor-follower"></div>

    <div id="loader" class="fixed inset-0 z-[100] bg-black flex flex-col items-center justify-center">
        <div class="text-center">
            <h1 id="loader-logo" class="text-4xl md:text-6xl font-bold tracking-[0.4em] mb-4 text-white">ASWAD</h1>
            <div class="w-48 h-[1px] bg-white/20 mx-auto relative overflow-hidden">
                <div id="loader-bar" class="absolute top-0 left-0 h-full bg-white w-0"></div>
            </div>
            <p class="mt-4 text-[10px] tracking-[0.3em] uppercase text-gray-500">Luxury Architecture & Streetwear</p>
        </div>
    </div>

    <nav id="navbar" class="fixed top-0 left-0 w-full z-50 py-8 transition-all duration-500">
        <div class="container mx-auto px-6 flex justify-between items-center">
            
            <div class="flex items-center gap-3 text-xs font-bold tracking-widest z-50">
                <button id="btn-lang-ar" onclick="setLanguage('ar')" class="text-white underline transition-colors">AR</button>
                <span class="text-white/20">|</span>
                <button id="btn-lang-en" onclick="setLanguage('en')" class="text-gray-500 transition-colors">EN</button>
            </div>

            <div class="hidden lg:flex gap-8 text-[11px] tracking-[0.2em] uppercase font-medium">
                <a href="#" onclick="scrollToSection('#products_section')" data-i18n="navNewIn" class="hover:opacity-50 transition-opacity">وصلنا حديثاً</a>
                <a href="#" onclick="scrollToSection('#products_section')" data-i18n="navHoodies" class="hover:opacity-50 transition-opacity">هوديز</a>
                <a href="#" onclick="scrollToSection('#products_section')" data-i18n="navOversized" class="hover:opacity-50 transition-opacity">فضفاض</a>
            </div>

            <div class="flex-shrink-0 text-center">
                <a href="#" onclick="scrollToSection('#hero_section')" class="text-2xl font-bold tracking-[0.4em]">ASWAD</a>
            </div>

            <div class="flex gap-6 items-center">
                <i data-lucide="menu" onclick="toggleMenuSidebar(true)" class="w-5 h-5 cursor-pointer hover:opacity-50"></i>
                <i data-lucide="search" onclick="openSearchModal()" class="w-5 h-5 cursor-pointer hover:opacity-50"></i>
                <i data-lucide="heart" class="w-5 h-5 cursor-pointer hover:opacity-50 hidden sm:block"></i>
                <div class="relative cursor-pointer hover:opacity-50" onclick="toggleCartSidebar(true)">
                    <i data-lucide="shopping-bag" class="w-5 h-5"></i>
                    <span class="cart-count absolute -top-1 -right-1 bg-white text-black text-[8px] font-bold w-3 h-3 rounded-full flex items-center justify-center">0</span>
                </div>
            </div>
        </div>
    </nav>

    <div id="menu-sidebar" class="fixed top-0 right-0 h-full w-full sm:w-[400px] bg-black border-l border-white/10 z-[65] shadow-2xl transition-all flex-col p-6 hidden">
        <div class="flex justify-between items-center pb-6 border-b border-white/10">
            <h3 data-i18n="menuSidebarTitle" class="text-sm font-bold tracking-[0.3em] uppercase text-white">الأقسام والمجموعات</h3>
            <button onclick="toggleMenuSidebar(false)" class="text-white hover:text-gray-400"><i data-lucide="x" class="w-5 h-5"></i></button>
        </div>
        
        <div class="flex flex-col gap-6 py-10 text-md tracking-[0.15em] uppercase font-light">
            <a href="#" onclick="toggleMenuSidebar(false); scrollToSection('#products_section')" data-i18n="catBoxFit" class="hover:pl-2 hover:text-gray-400 transition-all border-b border-white/5 pb-3 block">بوكس فيت</a>
            <a href="#" onclick="toggleMenuSidebar(false); scrollToSection('#products_section')" data-i18n="catOversized" class="hover:pl-2 hover:text-gray-400 transition-all border-b border-white/5 pb-3 block">أوفر سايز</a>
            <a href="#" onclick="toggleMenuSidebar(false); scrollToSection('#products_section')" data-i18n="catSweatpants" class="hover:pl-2 hover:text-gray-400 transition-all border-b border-white/5 pb-3 block">سويت بانتس</a>
            <a href="#" onclick="toggleMenuSidebar(false); scrollToSection('#products_section')" data-i18n="catCaps" class="hover:pl-2 hover:text-gray-400 transition-all border-b border-white/5 pb-3 block">كابات</a>
        </div>
    </div>
    <section id="hero_section" class="relative h-screen w-full flex items-center justify-center overflow-hidden">
        <div class="absolute inset-0 z-0">
            <div class="absolute inset-0 bg-black/40 z-10"></div>
            <img 
                src="https://images.unsplash.com/photo-1514813482567-2858e6c00ee1?auto=format&fit=crop&q=80&w=1920" 
                alt="Luxury Fashion Hero" 
                class="w-full h-full object-cover grayscale brightness-50 scale-110"
                id="hero-bg"
            >
        </div>

        <div class="relative z-20 text-center px-6">
            <p data-i18n="heroSub" class="reveal-up text-[10px] md:text-xs tracking-[0.6em] uppercase mb-8 opacity-70">أرشيف ربيع / صيف 2026</p>
            <h1 id="hero-main-title" data-i18n="heroTitle" class="reveal-up text-6xl md:text-[140px] font-bold tracking-tighter leading-none mb-12">
                حدد ملامح <span class="font-serif-italic font-light">الظمان</span>
            </h1>
            <div class="reveal-up flex flex-col sm:flex-row gap-6 justify-center items-center">
                <button onclick="scrollToSection('#products_section')" data-i18n="exploreBtn" class="px-12 py-5 bg-white text-black text-[10px] font-bold tracking-[0.3em] uppercase hover:bg-transparent hover:text-white border border-white transition-all duration-500">
                    اكتشف المجموعات
                </button>
                <button onclick="scrollToSection('#vanguard_section')" data-i18n="campaignBtn" class="px-12 py-5 border border-white/20 text-white text-[10px] font-bold tracking-[0.3em] uppercase hover:border-white transition-all duration-500">
                    فيلم الحملة
                </button>
            </div>
        </div>
    </section>

    <section id="products_section" class="py-32 bg-black">
        <div class="container mx-auto px-6">
            <div class="flex flex-col md:flex-row justify-between items-end mb-20">
                <div>
                    <h2 data-i18n="sectionTitle" class="reveal-up text-4xl md:text-6xl font-bold tracking-tighter uppercase mb-4">القطع المختارة</h2>
                    <p data-i18n="sectionSub" class="reveal-up text-gray-500 text-xs tracking-widest uppercase">صُممت لطليعة الليل.</p>
                </div>
                <a href="#" onclick="scrollToSection('#products_section')" data-i18n="viewAll" class="reveal-up hidden md:flex items-center gap-4 text-[10px] font-bold tracking-[0.3em] uppercase group">
                    عرض كل المجموعات <i data-lucide="arrow-right" class="w-4 h-4 group-hover:translate-x-2 transition-transform"></i>
                </a>
            </div>

            <div id="main-products-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-8"></div>
        </div>
    </section>

    <div id="product-details-modal" class="fixed inset-0 z-[70] bg-black/95 hidden items-center justify-center p-4 overflow-y-auto">
        <div id="details-card" class="bg-neutral-950 border border-white/10 w-full max-w-4xl p-6 md:p-8 rounded-sm relative max-h-[90vh] overflow-y-auto">
            <button onclick="closeProductDetails()" class="absolute top-4 left-4 md:left-6 text-white hover:text-gray-400 z-10">
                <i data-lucide="x" class="w-6 h-6"></i>
            </button>
            
            <div class="grid grid-cols-1 md:grid-cols-2 gap-8 items-start mt-4">
                <div class="grid grid-cols-2 gap-4 relative">
                    <img id="detail-img-1" src="" class="w-full aspect-[3/4] object-cover bg-black border border-white/5">
                    <div class="absolute top-0 bottom-0 left-1/2 w-[1px] bg-white/40 transform -translate-x-1/2 pointer-events-none"></div>
                    <img id="detail-img-2" src="" class="w-full aspect-[3/4] object-cover bg-black border border-white/5">
                </div>
                
                <div class="flex flex-col h-full justify-between">
                    <div>
                        <span id="detail-category" class="text-[9px] text-gray-500 tracking-widest uppercase block mb-2"></span>
                        <h2 id="detail-title" class="text-2xl font-bold tracking-wide uppercase text-white mb-4"></h2>
                        <p id="detail-price" class="text-xl font-light text-white mb-6"></p>
                        
                        <hr class="border-white/10 my-4">

                        <div class="mb-6">
                            <label class="block text-[10px] font-bold tracking-[0.2em] text-gray-400 uppercase mb-3" data-i18n="lblSize">المقاس المطلوب (SELECT SIZE)</label>
                            <div class="flex gap-2 flex-wrap" id="sizes-options-container">
                                <button onclick="selectProductSize(this, 'M')" class="size-btn border border-white/20 text-gray-400 px-4 py-2 text-xs font-bold bg-black hover:border-white transition-all duration-300">M</button>
                                <button onclick="selectProductSize(this, 'L')" class="size-btn border border-white/20 text-gray-400 px-4 py-2 text-xs font-bold bg-black hover:border-white transition-all duration-300">L</button>
                                <button onclick="selectProductSize(this, 'XL')" class="size-btn border border-white/20 text-gray-400 px-4 py-2 text-xs font-bold bg-black hover:border-white transition-all duration-300">XL</button>
                                <button onclick="selectProductSize(this, '2XL')" class="size-btn border border-white/20 text-gray-400 px-4 py-2 text-xs font-bold bg-black hover:border-white transition-all duration-300">2XL</button>
                            </div>
                        </div>

                        <div class="mb-6">
                            <label class="block text-[10px] font-bold tracking-[0.2em] text-gray-400 uppercase mb-3" data-i18n="lblColor">اللون (COLOR)</label>
                            <div class="flex items-center gap-2">
                                <span class="w-5 h-5 rounded-full bg-black border-2 border-white inline-block"></span>
                                <span class="text-xs text-white" data-i18n="colorBlack">أسود ملكي / Royal Black</span>
                            </div>
                        </div>
                    </div>

                    <button id="detail-add-btn" class="w-full bg-white text-black py-4 text-[11px] font-bold uppercase tracking-[0.2em] hover:bg-neutral-200 transition-colors mt-6">
                        + أضف للحقيبة
                    </button>
                </div>
            </div>
        </div>
    </div>

    <section class="relative h-[80vh] overflow-hidden bg-[#050505]">
        <div class="absolute inset-0 z-0">
            <img src="https://images.unsplash.com/photo-1509631179647-0177331693ae?auto=format&fit=crop&q=80&w=1920" class="w-full h-full object-cover grayscale contrast-125 scale-110">
        </div>
        <div class="absolute inset-0 bg-black/60 flex items-center justify-center text-center px-6">
            <div class="reveal-up max-w-4xl">
                <h2 data-i18n="campaignTitle" class="text-5xl md:text-8xl font-bold tracking-tight mb-8">الرقي البسيط</h2>
                <p data-i18n="campaignDesc" class="text-gray-400 max-w-lg mx-auto text-sm md:text-base mb-10 tracking-wide font-light">
                    كل تصميم هو استجابة مباشرة للبيئة المعمارية المحيطة. تلتقي البساطة مع الفخامة في أكثر مجموعاتنا تجريبية حتى الآن.
                </p>
                <a href="#" onclick="scrollToSection('#products_section')" data-i18n="viewStory" class="inline-block border-b border-white pb-2 text-[10px] font-bold tracking-[0.4em] uppercase hover:opacity-50 transition-opacity">عرض قصة الحملة</a>
            </div>
        </div>
    </section>

    <section id="vanguard_section" class="py-32 bg-black overflow-hidden">
        <div class="container mx-auto px-6">
            <div class="grid grid-cols-1 md:grid-cols-2 gap-20 items-center">
                <div class="reveal-up text-left">
                    <h3 data-i18n="followTitle" class="text-4xl md:text-6xl font-bold tracking-tighter mb-8">اتبع الطليعة</h3>
                    <p data-i18n="followDesc" class="text-gray-500 text-sm max-w-md mb-12 leading-loose">
                        ابق على اتصال مع مجتمعنا الإبداعي. احصل على وصول مبكر للقطع النادرة والفعاليات الخاصة عبر مركزنا الاجتماعي الأساسي.
                    </p>
                    <a href="https://linktr.ee/MohamedWaseem8" target="_blank" class="flex items-center gap-6 group">
                        <div class="w-16 h-16 rounded-full bg-white flex items-center justify-center text-black group-hover:scale-110 transition-transform duration-500">
                            <i data-lucide="external-link" class="w-6 h-6"></i>
                        </div>
                        <div>
                            <p data-i18n="hubTitle" class="text-[10px] tracking-[0.3em] text-gray-500 uppercase mb-1">المركز الرسمي</p>
                            <p class="text-lg font-medium">Linktree/@MohamedWaseem8</p>
                        </div>
                    </a>
                </div>
                <div class="reveal-up grid grid-cols-2 gap-4">
                    <div class="aspect-square bg-gray-900 overflow-hidden rounded-sm">
                        <img src="https://images.unsplash.com/photo-1515886657613-9f3515b0c78f?auto=format&fit=crop&q=80&w=800" class="w-full h-full object-cover grayscale hover:grayscale-0 transition-all duration-700">
                    </div>
                    <div class="aspect-square bg-gray-900 overflow-hidden rounded-sm mt-8">
                        <img src="https://images.unsplash.com/photo-1539109136881-3be0616acf4b?auto=format&fit=crop&q=80&w=800" class="w-full h-full object-cover grayscale hover:grayscale-0 transition-all duration-700">
                    </div>
                </div>
            </div>
        </div>
    </section>

    <footer class="py-24 border-t border-white/10 bg-[#020202]">
        <div class="container mx-auto px-6 text-left">
            <div class="grid grid-cols-1 md:grid-cols-4 gap-12 text-left">
                <div>
                    <h2 class="text-2xl font-bold tracking-[0.4em] mb-8">ASWAD</h2>
                    <p data-i18n="footerDesc" class="text-gray-500 text-xs leading-loose max-w-xs">ملابس الشارع الراقية لأصحاب الليل. صُممت في مصر، وفُصِّلت للعالم.</p>
                </div>
                <div>
                    <h4 data-i18n="footerArchive" class="text-[10px] font-bold tracking-[0.3em] uppercase mb-8 text-gray-400">الأرشيف</h4>
                    <ul class="space-y-4 text-[11px] text-gray-600 tracking-widest uppercase">
                        <li><a href="#" onclick="scrollToSection('#products_section')" data-i18n="shopAll" class="hover:text-white transition-colors">تسوق الكل</a></li>
                    </ul>
                </div>
                <div>
                    <h4 data-i18n="footerHelp" class="text-[10px] font-bold tracking-[0.3em] uppercase mb-8 text-gray-400">المساعدة</h4>
                    <ul class="space-y-4 text-[11px] text-gray-600 tracking-widest uppercase">
                        <li><a href="#" data-i18n="shipping" class="hover:text-white transition-colors">الشحن والتوصيل</a></li>
                    </ul>
                </div>
                <div>
                    <h4 data-i18n="footerConnect" class="text-[10px] font-bold tracking-[0.3em] uppercase mb-8 text-gray-400">اتصل بنا</h4>
                    <ul class="space-y-4 text-[11px] text-gray-600 tracking-widest uppercase">
                        <li><a href="https://linktr.ee/MohamedWaseem8" target="_blank" class="hover:text-white transition-colors">Linktree</a></li>
                    </ul>
                </div>
            </div>
        </div>
    </footer>

    <div id="cart-sidebar
