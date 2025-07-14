<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kweek Tess Fashion - Aapka Style, Aapki Pehchan</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;900&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
    <!-- Swiper.js CSS -->
    <link rel="stylesheet" href="https://unpkg.com/swiper/swiper-bundle.min.css" />
    <style>
        body { font-family: 'Inter', sans-serif; background-color: #f9fafb; }
        .product-card .product-image { position: relative; overflow: hidden; border-radius: 0.5rem; cursor: pointer; }
        .product-card { transition: transform 0.3s ease, box-shadow 0.3s ease; }
        .product-card:hover { transform: translateY(-5px); box-shadow: 0 10px 15px -3px rgba(0,0,0,.1), 0 4px 6px -4px rgba(0,0,0,.1); }
        .size-option { border: 1px solid #d1d5db; transition: all 0.2s; }
        .size-option:hover, .size-option.selected { background-color: #1f2937; color: white; border-color: #1f2937; }
        .add-to-cart-btn { background-color: #3b82f6; transition: background-color 0.3s; }
        .add-to-cart-btn:hover { background-color: #2563eb; }
        .form-input { border: 1px solid #d1d5db; border-radius: 0.5rem; padding: 0.75rem 1rem; width: 100%; transition: border-color 0.2s, box-shadow 0.2s; }
        .form-input:focus { outline: none; border-color: #3b82f6; box-shadow: 0 0 0 2px rgba(59, 130, 246, 0.4); }
        #place-order-btn:disabled { background-color: #9ca3af; cursor: not-allowed; }
        .hero-section { background: url('https://images.unsplash.com/photo-1489987707025-afc232f7ea0f?q=80&w=2070&auto=format&fit=crop') center center/cover no-repeat; }
        .category-card:hover { transform: translateY(-5px); box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05); }
        .swiper-container { width: 100%; height: 40vh; margin-bottom: 2rem; border-radius: 0.5rem; }
        .swiper-slide img { width: 100%; height: 100%; object-fit: cover; }
        .swiper-button-next, .swiper-button-prev { color: #ffffff; }
        .subcategory-icon:hover { transform: scale(1.05); }
        .thumbnail { cursor: pointer; border: 2px solid transparent; transition: border-color 0.3s; }
        .thumbnail.active, .thumbnail:hover { border-color: #3b82f6; }
        .search-suggestion:hover { background-color: #f3f4f6; }

        /* Animation Styles */
        .animated-section {
            opacity: 0;
            transform: translateY(30px);
            transition: opacity 0.6s ease-out, transform 0.6s ease-out;
        }
        .animated-section.is-visible {
            opacity: 1;
            transform: translateY(0);
        }
        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }
        .pulse-btn {
            animation: pulse 2s infinite;
        }
    </style>
</head>
<body class="text-gray-800">

    <!-- Header -->
    <header class="bg-white shadow-sm sticky top-0 z-50">
        <nav class="container mx-auto px-4 sm:px-6 py-3 flex justify-between items-center">
            <button id="mobile-menu-button" class="md:hidden text-gray-700 hover:text-gray-900"><i class="fas fa-bars text-2xl"></i></button>
            <a href="#" class="logo-link text-2xl md:text-3xl font-bold text-gray-900 absolute left-1/2 -translate-x-1/2">Kweek Tess</a>
            <div class="flex items-center space-x-4 sm:space-x-6">
                <button id="search-icon-btn" class="text-gray-700 hover:text-gray-900"><i class="fas fa-search text-xl"></i></button>
                <a href="#" class="text-gray-700 hover:text-gray-900"><i class="fas fa-user text-xl"></i></a>
                <a href="#" id="cart-icon" class="relative text-gray-700 hover:text-gray-900">
                    <i class="fas fa-shopping-cart text-xl"></i>
                    <span id="cart-count" class="absolute -top-2 -right-2 bg-red-500 text-white text-xs rounded-full h-5 w-5 flex items-center justify-center">0</span>
                </a>
            </div>
        </nav>
        <div id="desktop-nav" class="hidden md:flex justify-center items-center space-x-8 py-2 border-t border-gray-200">
            <a href="#" class="nav-link text-gray-600 hover:text-gray-900 font-medium" data-page="home-page">Home</a>
            <a href="#" class="nav-link text-gray-600 hover:text-gray-900 font-medium" data-page="products-page">T-Shirts</a>
            <a href="#" class="nav-link text-gray-600 hover:text-gray-900 font-medium" data-page="jeans-page">Jeans</a>
        </div>
        <div id="mobile-menu" class="hidden md:hidden bg-white px-6 pb-4 border-t">
            <a href="#" class="nav-link block py-2 text-gray-600 hover:text-gray-900" data-page="home-page">Home</a>
            <a href="#" class="nav-link block py-2 text-gray-600 hover:text-gray-900" data-page="products-page">T-Shirts</a>
            <a href="#" class="nav-link block py-2 text-gray-600 hover:text-gray-900" data-page="jeans-page">Jeans</a>
        </div>
    </header>

    <!-- Search Modal -->
    <div id="search-modal" class="hidden fixed inset-0 bg-black bg-opacity-50 z-[100] flex justify-center items-start pt-20">
        <div class="bg-white rounded-lg shadow-xl w-full max-w-2xl mx-4">
            <div class="p-4 border-b flex items-center">
                <i class="fas fa-search text-gray-400 mr-3"></i>
                <input type="text" id="search-input" placeholder="Search for products..." class="w-full focus:outline-none text-lg">
                <button id="close-search-btn" class="text-2xl text-gray-500 hover:text-gray-800">&times;</button>
            </div>
            <div id="search-suggestions" class="max-h-96 overflow-y-auto">
                <!-- Search suggestions will be populated here -->
            </div>
        </div>
    </div>

    <!-- Home Page -->
    <main id="home-page" class="page-container">
        <section class="hero-section text-white bg-gray-800">
            <div class="container mx-auto px-6 py-32 text-center bg-black bg-opacity-50">
                <h1 class="text-4xl md:text-6xl font-extrabold tracking-tight mb-4">Kweek Tess Fashion</h1>
                <p class="text-lg md:text-xl mb-8 max-w-2xl mx-auto">Aapka Style, Aapki Pehchan. Discover the new you.</p>
                <a href="#" class="nav-link pulse-btn bg-red-500 hover:bg-red-600 text-white font-bold py-3 px-8 rounded-full transition duration-300 text-lg" data-page="products-page">Shop Now</a>
            </div>
        </section>
        <section class="py-16 bg-white animated-section">
            <div class="container mx-auto px-6 text-center">
                <h2 class="text-3xl font-bold mb-4">About Kweek Tess</h2>
                <p class="text-gray-600 max-w-3xl mx-auto">Kweek Tess Fashion mein humara maksad hai aap tak high-quality aur trendy clothes pahuchana. Humara har product behtareen material se bana hai aur comfort aur style ka perfect blend hai.</p>
            </div>
        </section>
        <section class="py-16 animated-section">
            <div class="container mx-auto px-6">
                <h2 class="text-3xl font-bold text-center mb-10">Our Collections</h2>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                    <div class="category-card rounded-lg overflow-hidden relative nav-link cursor-pointer" data-page="products-page"><img src="https://images.unsplash.com/photo-1527719327859-c6ce80353573?q=80&w=1964&auto=format&fit=crop" alt="T-Shirts Collection" class="w-full h-80 object-cover"><div class="absolute inset-0 bg-black bg-opacity-40 flex items-center justify-center"><h3 class="text-white text-3xl font-bold">T-Shirts</h3></div></div>
                    <div class="category-card rounded-lg overflow-hidden relative nav-link cursor-pointer" data-page="jeans-page"><img src="https://images.unsplash.com/photo-1602293589914-9e296ba2a7c4?q=80&w=1887&auto=format&fit=crop" alt="Jeans Collection" class="w-full h-80 object-cover"><div class="absolute inset-0 bg-black bg-opacity-40 flex items-center justify-center"><h3 class="text-white text-3xl font-bold">Jeans</h3></div></div>
                </div>
            </div>
        </section>
    </main>

    <!-- Products Page (Main T-shirt page) -->
    <main id="products-page" class="page-container hidden container mx-auto px-4 sm:px-6 py-8">
        <div class="swiper-container rounded-lg overflow-hidden">
            <div class="swiper-wrapper">
                <div class="swiper-slide"><img src="https://images.unsplash.com/photo-1574180566258-5545cf0b345b?q=80&w=2070&auto=format&fit=crop" alt="Fashion Banner 1"></div>
                <div class="swiper-slide"><img src="https://images.unsplash.com/photo-1556905055-8f358a7a47b2?q=80&w=2070&auto=format&fit=crop" alt="Fashion Banner 2"></div>
                <div class="swiper-slide"><img src="https://images.unsplash.com/photo-1490481651871-ab68de25d43d?q=80&w=2070&auto=format&fit=crop" alt="Fashion Banner 3"></div>
            </div>
            <div class="swiper-pagination"></div><div class="swiper-button-next"></div><div class="swiper-button-prev"></div>
        </div>
        <section class="py-8 animated-section"><div class="grid grid-cols-2 md:grid-cols-4 gap-4 md:gap-8 text-center" id="subcategory-icons"></div></section>
        <div class="flex flex-col md:flex-row justify-between items-center mb-8 border-t pt-8 animated-section"><h1 class="text-2xl font-bold text-gray-900 mb-4 md:mb-0">All T-Shirts</h1></div>
        <section id="all-products-grid" class="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-4 gap-4 md:gap-6 animated-section"></section>
    </main>
    
    <!-- Sub-Category Pages (e.g., Round Neck) -->
    <main id="subcategory-page" class="page-container hidden container mx-auto px-4 sm:px-6 py-8">
        <div class="flex justify-between items-center mb-8">
            <h1 id="subcategory-title" class="text-3xl font-bold text-gray-900"></h1>
            <button class="nav-link text-blue-600 hover:underline font-semibold" data-page="products-page">&larr; Back to All T-Shirts</button>
        </div>
        <div id="subcategory-grid" class="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-5 gap-4 md:gap-6"></div>
    </main>
    
    <!-- Jeans Page -->
    <main id="jeans-page" class="page-container hidden container mx-auto px-4 sm:px-6 py-8">
         <div class="text-center py-16 animated-section">
            <i class="fas fa-wrench text-6xl text-gray-400 mb-4"></i>
            <h1 class="text-4xl font-bold text-gray-800">Jeans Collection</h1>
            <p class="text-gray-500 text-lg mt-2">Coming Soon!</p>
        </div>
    </main>

    <!-- Product Detail Page -->
    <main id="product-detail-page" class="page-container hidden container mx-auto px-4 sm:px-6 py-8">
        <button id="back-to-products-btn" class="text-blue-600 hover:underline font-semibold mb-6">&larr; Back to products</button>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-12 animated-section">
            <!-- Image Gallery -->
            <div>
                <img id="main-product-image" src="" alt="Product Image" class="w-full rounded-lg shadow-lg mb-4">
                <div id="thumbnail-gallery" class="grid grid-cols-5 gap-2"></div>
            </div>
            <!-- Product Info -->
            <div>
                <h1 id="product-detail-name" class="text-4xl font-bold mb-2"></h1>
                <p id="product-detail-price" class="text-3xl text-gray-800 mb-6"></p>
                <div class="mb-6">
                    <h3 class="font-semibold text-lg mb-2">Description</h3>
                    <p id="product-detail-desc" class="text-gray-600"></p>
                </div>
                <div class="mb-6">
                    <h3 class="font-semibold text-lg mb-2">Select Size</h3>
                    <div id="product-detail-sizes" class="flex space-x-2"></div>
                </div>
                <button id="product-detail-add-to-cart" class="w-full bg-blue-500 text-white font-bold py-3 px-4 rounded-lg hover:bg-blue-600 transition">Add to Cart</button>
            </div>
        </div>
    </main>

    <!-- Cart Page, Checkout Page, Confirmation Page -->
    <section id="cart-page" class="page-container hidden container mx-auto px-4 sm:px-6 py-8"><h1 class="text-3xl font-bold text-gray-900 mb-8">Your Shopping Cart</h1><div id="cart-content"></div></section>
    <section id="checkout-page" class="page-container hidden container mx-auto px-4 sm:px-6 py-8"><h1 class="text-3xl font-bold text-gray-900 mb-8">Checkout</h1><div class="flex flex-col lg:flex-row gap-12"><div class="flex-grow lg:w-3/5 bg-white p-8 rounded-lg shadow-md"><h2 class="text-2xl font-semibold mb-6">Shipping Address</h2><form id="checkout-form" class="space-y-6"><div><label for="fullName" class="block text-sm font-medium text-gray-700 mb-1">Pura Naam</label><input type="text" id="fullName" name="Customer Name" class="form-input" required></div><div><label for="address" class="block text-sm font-medium text-gray-700 mb-1">Pata</label><input type="text" id="address" name="Address" class="form-input" required></div><div><label for="city" class="block text-sm font-medium text-gray-700 mb-1">Shahar</label><input type="text" id="city" name="City" class="form-input" required></div><div class="flex gap-4"><div class="flex-1"><label for="pincode" class="block text-sm font-medium text-gray-700 mb-1">Pin Code</label><input type="text" id="pincode" name="Pincode" class="form-input" required></div><div class="flex-1"><label for="phone" class="block text-sm font-medium text-gray-700 mb-1">Mobile Number</label><input type="tel" id="phone" name="Phone" class="form-input" required></div></div></form></div><div id="checkout-summary" class="lg:w-2/5"></div></div></section>
    <section id="confirmation-page" class="page-container hidden container mx-auto px-4 sm:px-6 py-16 text-center">
        <div class="bg-white p-10 rounded-lg shadow-lg max-w-md mx-auto">
            <i class="fas fa-check-circle text-6xl text-green-500 mb-6"></i>
            <h1 class="text-3xl font-bold text-gray-800 mb-2">Thank You!</h1>
            <p class="text-gray-600 text-lg">Aapka order safaltapurvak place ho gaya hai.</p>
            <p class="text-gray-500 mt-4">Jald hi aapko confirmation email milega.</p>
            <button id="back-to-home-btn" class="mt-8 bg-blue-500 text-white font-bold py-3 px-8 rounded-full hover:bg-blue-600 transition">Continue Shopping</button>
        </div>
    </section>

    <!-- Footer -->
    <footer class="bg-gray-800 text-white mt-12">
        <div class="container mx-auto px-6 py-10 text-center"><p>&copy; 2024 Kweek Tess Fashion. All Rights Reserved.</p></div>
    </footer>
    
    <!-- Temporary Copyright - Isko baad mein hata sakte hain -->
    <div class="bg-black text-white text-center py-2 text-sm">
        Designed by Ritik
    </div>
    
    <div id="notification-container" class="fixed bottom-5 right-5 z-50"></div>

    <!-- Swiper.js JS -->
    <script src="https://unpkg.com/swiper/swiper-bundle.min.js"></script>
    <script>
    document.addEventListener('DOMContentLoaded', () => {

        // --- DATABASE ---
        const db = {
            products: [
                // Round Neck
                { id: 101, name: "Classic Black Round Neck", price: 449, subcategory: "Round Neck", images: ["https://images.unsplash.com/photo-1583743814966-8936f5b7be1a?w=800", "https://images.unsplash.com/photo-1622470953794-3150722c15b1?w=800", "https://images.unsplash.com/photo-1618354691373-d851c5c3a990?w=800"], sizes: ["S", "M", "L"], desc: "100% Cotton fabric. Regular fit for maximum comfort. Perfect for daily wear." },
                { id: 102, name: "White Graphic Tee", price: 549, subcategory: "Round Neck", images: ["https://images.unsplash.com/photo-1521572163474-6864f9cf17ab?w=800", "https://images.unsplash.com/photo-1503341504253-dff48986257f?w=800"], sizes: ["M", "L", "XL"], desc: "High-quality graphic print on soft cotton. A perfect style statement." },
                { id: 103, name: "Navy Blue Solid", price: 499, subcategory: "Round Neck", images: ["https://images.unsplash.com/photo-1622470953794-3150722c15b1?w=800", "https://images.unsplash.com/photo-1583743814966-8936f5b7be1a?w=800"], sizes: ["S", "L", "XL"], desc: "A classic navy blue t-shirt that never goes out of style. Made with premium combed cotton." },
                { id: 104, name: "Olive Green Tee", price: 479, subcategory: "Round Neck", images: ["https://images.unsplash.com/photo-1576566588028-4147f3842f27?w=800", "https://images.unsplash.com/photo-1618354691373-d851c5c3a990?w=800"], sizes: ["M", "L"], desc: "Stylish olive green t-shirt, perfect for a casual day out. Bio-washed for a soft feel." },
                { id: 105, name: "Maroon Round Neck", price: 499, subcategory: "Round Neck", images: ["https://images.unsplash.com/photo-1618354691373-d851c5c3a990?w=800", "https://images.unsplash.com/photo-1583743814966-8936f5b7be1a?w=800"], sizes: ["S", "M", "XL"], desc: "Rich maroon color for a bold look. Lightweight and comfortable for all-day wear." },
                
                // Oversize
                { id: 201, name: "Street Style Oversize", price: 799, subcategory: "Oversize", images: ["https://images.unsplash.com/photo-1503341733017-190157e5e1c9?w=800", "https://images.unsplash.com/photo-1529374255404-311a2a4f1fd9?w=800"], sizes: ["M", "L"], desc: "Trendy oversize fit for a cool, street-style look. Made with breathable fabric." },
                { id: 202, name: "Baggy Fit Graphic", price: 849, subcategory: "Oversize", images: ["https://images.unsplash.com/photo-1582898997534-187515a23735?w=800", "https://images.unsplash.com/photo-1633215882193-5a7a5b35e4e7?w=800"], sizes: ["L", "XL"], desc: "Express yourself with this baggy fit graphic tee. Perfect for a relaxed and cool vibe." },
                { id: 203, name: "Relaxed Fit Plain", price: 699, subcategory: "Oversize", images: ["https://images.unsplash.com/photo-1564589292024-74b73a4a75b8?w=800", "https://images.unsplash.com/photo-1503341733017-190157e5e1c9?w=800"], sizes: ["S", "M", "L"], desc: "A simple yet stylish relaxed fit t-shirt for ultimate comfort. Your new wardrobe staple." },
                { id: 204, name: "Drop Shoulder Tee", price: 759, subcategory: "Oversize", images: ["https://images.unsplash.com/photo-1633215882193-5a7a5b35e4e7?w=800", "https://images.unsplash.com/photo-1582898997534-187515a23735?w=800"], sizes: ["M", "L", "XL"], desc: "Modern drop shoulder design for a fashionable silhouette. Made with heavy-gauge cotton." },
                { id: 206, name: "Kweek Tess Graphic Oversize", price: 99, originalPrice: 1000, subcategory: "Oversize", images: ["https://res.cloudinary.com/dtjjgiitl/image/upload/q_auto:good,f_auto,fl_progressive/v1752442935/dzxswo1zb2dmty81blja.jpg", "https://images.unsplash.com/photo-1503341733017-190157e5e1c9?w=800", "https://images.unsplash.com/photo-1529374255404-311a2a4f1fd9?w=800"], sizes: ["S", "M", "L", "XL"], desc: "Stand out from the crowd with this trendy graphic oversize t-shirt from Kweek Tess. Made from premium soft cotton, it offers a relaxed fit for all-day comfort and a bold statement look." },

                // Full Sleeve
                { id: 301, name: "Henley Full Sleeve", price: 649, subcategory: "Full Sleeve", images: ["https://images.unsplash.com/photo-1611312449412-6cefac5dc3e4?w=800", "https://images.unsplash.com/photo-1620799140408-edc6dcb6d633?w=800"], sizes: ["S", "M", "L"], desc: "Classic Henley neck with full sleeves. Versatile and stylish for any occasion." },
                { id: 302, name: "Striped Long Sleeve", price: 699, subcategory: "Full Sleeve", images: ["https://images.unsplash.com/photo-1568306107998-6d27a7b11e23?w=800", "https://images.unsplash.com/photo-1600185365926-3a2ce3cdb9eb?w=800"], sizes: ["M", "L", "XL"], desc: "Timeless stripes on a comfortable long sleeve t-shirt. Perfect for layering." },
                { id: 303, name: "Solid Black Full", price: 599, subcategory: "Full Sleeve", images: ["https://images.unsplash.com/photo-1523381294911-8d3cead13475?w=800", "https://images.unsplash.com/photo-1611312449412-6cefac5dc3e4?w=800"], sizes: ["S", "M"], desc: "An essential solid black full sleeve t-shirt for every wardrobe. Soft and durable." },
                { id: 304, name: "Raglan Sleeve Tee", price: 749, subcategory: "Full Sleeve", images: ["https://images.unsplash.com/photo-1620799140408-edc6dcb6d633?w=800", "https://images.unsplash.com/photo-1568306107998-6d27a7b11e23?w=800"], sizes: ["L", "XL"], desc: "Sporty raglan sleeves in contrasting colors. A great choice for a casual, athletic look." },
                { id: 305, name: "Grey Full Sleeve", price: 629, subcategory: "Full Sleeve", images: ["https://images.unsplash.com/photo-1600185365926-3a2ce3cdb9eb?w=800", "https://images.unsplash.com/photo-1523381294911-8d3cead13475?w=800"], sizes: ["S", "M", "L"], desc: "Versatile grey full sleeve t-shirt. Pairs well with any jeans or trousers." },

                // Half Sleeve
                { id: 401, name: "Polo Half Sleeve", price: 599, subcategory: "Half Sleeve", images: ["https://images.unsplash.com/photo-1571455789372-2cebe5015427?w=800", "https://images.unsplash.com/photo-1554568218-0f1715e72254?w=800"], sizes: ["M", "L", "XL"], desc: "Smart and casual Polo T-shirt. Made with premium piqué fabric." },
                { id: 402, name: "V-Neck Half Sleeve", price: 499, subcategory: "Half Sleeve", images: ["https://images.unsplash.com/photo-1554568218-0f1715e72254?w=800", "https://images.unsplash.com/photo-1571455789372-2cebe5015427?w=800"], sizes: ["S", "M"], desc: "A modern V-neck t-shirt for a sharp look. Soft, breathable, and comfortable." },
                { id: 403, name: "Printed Half Sleeve", price: 549, subcategory: "Half Sleeve", images: ["https://images.unsplash.com/photo-1503341504253-dff48986257f?w=800", "https://images.unsplash.com/photo-1621353240202-a1b9d479195a?w=800"], sizes: ["M", "L", "XL"], desc: "Fun and quirky print on a classic half sleeve tee. Show off your personality." },
                { id: 404, name: "Teal Blue Tee", price: 489, subcategory: "Half Sleeve", images: ["https://images.unsplash.com/photo-1621353240202-a1b9d479195a?w=800", "https://images.unsplash.com/photo-1626497764746-6dc36844b428?w=800"], sizes: ["S", "L"], desc: "A refreshing teal blue t-shirt to brighten up your day. Made from 100% cotton." },
                { id: 405, name: "Yellow Plain Tee", price: 459, subcategory: "Half Sleeve", images: ["https://images.unsplash.com/photo-1626497764746-6dc36844b428?w=800", "https://images.unsplash.com/photo-1503341504253-dff48986257f?w=800"], sizes: ["M", "L"], desc: "A bright and cheerful yellow t-shirt. Perfect for summer and casual outings." },
            ],
            subcategories: [
                { id: "round-neck", name: "Round Neck", icon: `<svg class="h-12 w-12" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v-4a2 2 0 012-2h12a2 2 0 012 2v4M12 10V4M8 4h8"/></svg>` },
                { id: "oversize", name: "Oversize", icon: `<svg class="h-12 w-12" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 10h18M3 14h18M9 4v16M15 4v16"/></svg>` },
                { id: "full-sleeve", name: "Full Sleeve", icon: `<svg class="h-12 w-12" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v-4a2 2 0 012-2h12a2 2 0 012 2v4M12 10V4M8 4h8M4.055 16.055L4 20h16l-.055-3.945"/></svg>` },
                { id: "half-sleeve", name: "Half Sleeve", icon: `<svg class="h-12 w-12" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v-4a2 2 0 012-2h12a2 2 0 012 2v4M12 10V4M8 4h8M6 16v-2m12 2v-2"/></svg>` },
            ]
        };
        let lastSubcategory = 'products-page';
        let cartItems = [];

        // --- PAGE NAVIGATION ---
        const showPage = (pageId, context = {}) => {
            document.querySelectorAll('.page-container').forEach(p => p.classList.add('hidden'));
            const targetPage = document.getElementById(pageId);
            if (targetPage) {
                window.scrollTo(0, 0);
                targetPage.classList.remove('hidden');
                document.getElementById('desktop-nav').classList.toggle('hidden', pageId === 'checkout-page' || pageId === 'confirmation-page');
                
                if (pageId === 'subcategory-page') {
                    lastSubcategory = context.subcategory;
                    renderSubCategoryPage(context.subcategory);
                } else if (pageId === 'product-detail-page') {
                    renderProductDetailPage(context.productId);
                } else if(pageId === 'products-page') {
                    lastSubcategory = 'products-page';
                }
            }
        };
        
        // --- RENDERING FUNCTIONS ---
        const createProductCardHTML = (product) => {
            const priceHTML = product.originalPrice
                ? `<div class="flex items-baseline justify-center space-x-2 mt-2">
                       <p class="font-bold text-lg text-red-500">₹${product.price}</p>
                       <p class="text-sm text-gray-500 line-through">₹${product.originalPrice}</p>
                   </div>`
                : `<p class="font-bold text-lg mt-2">₹${product.price}</p>`;
            return `
                <div class="product-card bg-white rounded-lg group text-center flex flex-col" data-id="${product.id}">
                    <div class="product-image" data-product-id="${product.id}">
                        <img src="${product.images[0]}" onerror="this.onerror=null;this.src='https://placehold.co/400x500/e5e7eb/4b5563?text=No+Image';" alt="${product.name}" class="w-full h-64 object-cover">
                    </div>
                    <div class="p-3 md:p-4 flex flex-col flex-grow">
                        <h3 class="font-medium truncate">${product.name}</h3>
                        ${priceHTML}
                    </div>
                </div>`;
        };

        const renderSubCategoryIcons = () => {
            const container = document.getElementById('subcategory-icons');
            container.innerHTML = db.subcategories.map(cat => `
                <div class="subcategory-icon nav-link cursor-pointer" data-page="subcategory-page" data-context='${JSON.stringify({subcategory: cat.name})}'>
                    <div class="icon-wrapper p-4 rounded-full shadow-md w-24 h-24 mx-auto flex items-center justify-center">${cat.icon}</div>
                    <h3 class="mt-3 font-semibold">${cat.name}</h3>
                </div>
            `).join('');
            setupNavLinks();
        };

        const renderSubCategoryPage = (subcategoryName) => {
            document.getElementById('subcategory-title').textContent = `${subcategoryName} T-Shirts`;
            const products = db.products.filter(p => p.subcategory === subcategoryName);
            const grid = document.getElementById('subcategory-grid');
            grid.innerHTML = products.length > 0 ? products.map(createProductCardHTML).join('') : '<p>No products in this category yet.</p>';
            setupProductCardEventListeners();
        };

        const renderProductDetailPage = (productId) => {
            const product = db.products.find(p => p.id === productId);
            if (!product) return;

            document.getElementById('main-product-image').src = product.images[0];
            document.getElementById('product-detail-name').textContent = product.name;
            
            const priceDetailContainer = document.getElementById('product-detail-price');
            priceDetailContainer.innerHTML = product.originalPrice
                ? `<span class="text-4xl font-bold text-red-500">₹${product.price}</span>
                   <span class="text-xl text-gray-500 line-through ml-3">₹${product.originalPrice}</span>`
                : `<span class="text-3xl text-gray-800">₹${product.price}</span>`;

            document.getElementById('product-detail-desc').textContent = product.desc;

            const thumbnailContainer = document.getElementById('thumbnail-gallery');
            thumbnailContainer.innerHTML = product.images.map((img, index) => `
                <img src="${img}" alt="Thumbnail ${index + 1}" class="thumbnail ${index === 0 ? 'active' : ''} w-full h-24 object-cover rounded-md">
            `).join('');
            
            thumbnailContainer.querySelectorAll('.thumbnail').forEach(thumb => {
                thumb.addEventListener('click', () => {
                    document.getElementById('main-product-image').src = thumb.src;
                    thumbnailContainer.querySelectorAll('.thumbnail').forEach(t => t.classList.remove('active'));
                    thumb.classList.add('active');
                });
            });

            const sizesContainer = document.getElementById('product-detail-sizes');
            sizesContainer.innerHTML = product.sizes.map(size => `<span class="size-option text-sm font-medium w-10 h-10 flex items-center justify-center rounded-md cursor-pointer">${size}</span>`).join('');
            
            const addToCartBtn = document.getElementById('product-detail-add-to-cart');
            addToCartBtn.onclick = () => {
                const selectedSizeEl = sizesContainer.querySelector('.size-option.selected');
                if (!selectedSizeEl) {
                    showNotification('Please select a size first!', 'error');
                    return;
                }
                addToCart({
                    id: product.id,
                    name: product.name,
                    price: product.price,
                    image: product.images[0],
                    size: selectedSizeEl.textContent
                });
            };
            
            sizesContainer.querySelectorAll('.size-option').forEach(opt => {
                opt.addEventListener('click', () => {
                    sizesContainer.querySelectorAll('.size-option').forEach(s => s.classList.remove('selected'));
                    opt.classList.add('selected');
                });
            });
        };
        
        const renderAllProductsGrid = () => {
            const grid = document.getElementById('all-products-grid');
            grid.innerHTML = db.products.length > 0 ? db.products.map(createProductCardHTML).join('') : '<p>Loading products...</p>';
            setupProductCardEventListeners();
        };

        // --- EVENT LISTENERS & INITIALIZATION ---
        const setupNavLinks = () => {
            document.querySelectorAll('.nav-link, .logo-link').forEach(link => {
                if(link.dataset.navListener) return;
                link.dataset.navListener = 'true';
                link.addEventListener('click', (e) => {
                    e.preventDefault();
                    const pageId = e.currentTarget.dataset.page;
                    const context = e.currentTarget.dataset.context ? JSON.parse(e.currentTarget.dataset.context) : {};
                    showPage(pageId || 'home-page', context);
                });
            });
        };

        const setupProductCardEventListeners = () => {
             document.querySelectorAll('.product-image').forEach(cardImage => {
                if (cardImage.dataset.listener) return;
                cardImage.dataset.listener = 'true';
                cardImage.addEventListener('click', (e) => {
                    const productId = parseInt(e.currentTarget.dataset.productId, 10);
                    showPage('product-detail-page', { productId });
                });
            });
        };
        
        const setupEventListeners = () => {
            setupNavLinks();
            setupProductCardEventListeners();

            document.getElementById('back-to-products-btn').addEventListener('click', () => {
                if (lastSubcategory && lastSubcategory !== 'products-page') {
                    showPage('subcategory-page', { subcategory: lastSubcategory });
                } else {
                    showPage('products-page');
                }
            });

            document.getElementById('cart-icon').addEventListener('click', (e) => {
                e.preventDefault();
                renderCartPage();
                showPage('cart-page');
            });

            document.getElementById('mobile-menu-button').addEventListener('click', () => {
                document.getElementById('mobile-menu').classList.toggle('hidden');
            });

            // Search
            const searchModal = document.getElementById('search-modal');
            const searchInput = document.getElementById('search-input');
            document.getElementById('search-icon-btn').addEventListener('click', () => searchModal.classList.remove('hidden'));
            document.getElementById('close-search-btn').addEventListener('click', () => searchModal.classList.add('hidden'));
            searchModal.addEventListener('click', (e) => { if(e.target === searchModal) searchModal.classList.add('hidden'); });
            searchInput.addEventListener('input', handleSearchInput);
            
            document.getElementById('back-to-home-btn').addEventListener('click', () => showPage('home-page'));
        };
        
        const handleSearchInput = () => {
            const query = document.getElementById('search-input').value.toLowerCase();
            const suggestionsContainer = document.getElementById('search-suggestions');
            if (query.length < 1) {
                suggestionsContainer.innerHTML = '';
                return;
            }
            
            const filteredProducts = db.products.filter(p => p.name.toLowerCase().includes(query)).slice(0, 5);
            const filteredCategories = db.subcategories.filter(c => c.name.toLowerCase().includes(query));

            let html = '';

            if (filteredCategories.length > 0) {
                html += '<h3 class="font-bold text-gray-500 px-4 pt-4 pb-2 text-sm">Categories</h3>';
                html += filteredCategories.map(cat => `
                    <div class="search-suggestion nav-link p-4 cursor-pointer flex items-center" data-page="subcategory-page" data-context='${JSON.stringify({subcategory: cat.name})}'>
                        ${cat.icon.replace('h-12 w-12', 'h-6 w-6 mr-3')}
                        <span>${cat.name}</span>
                    </div>
                `).join('');
            }
            
            if (filteredProducts.length > 0) {
                html += '<h3 class="font-bold text-gray-500 px-4 pt-4 pb-2 text-sm">Products</h3>';
                html += filteredProducts.map(p => `
                    <div class="search-suggestion product-image p-4 cursor-pointer flex items-center" data-product-id="${p.id}">
                        <img src="${p.images[0]}" class="w-10 h-10 object-cover rounded-md mr-4">
                        <span>${p.name}</span>
                    </div>
                `).join('');
            }

            suggestionsContainer.innerHTML = html || '<p class="p-4 text-gray-500">No results found.</p>';
            setupNavLinks();
            setupProductCardEventListeners();
            suggestionsContainer.querySelectorAll('.nav-link, .product-image').forEach(el => el.addEventListener('click', () => document.getElementById('search-modal').classList.add('hidden')));
        };


        // --- CART & CHECKOUT LOGIC (Same as before) ---
        const showNotification = (message, type = 'success') => { const container = document.getElementById('notification-container'); const bgColor = type === 'success' ? 'bg-green-500' : 'bg-red-500'; const notification = document.createElement('div'); notification.className = `${bgColor} text-white py-3 px-5 rounded-lg shadow-lg mb-2 animate-pulse`; notification.textContent = message; container.appendChild(notification); setTimeout(() => notification.remove(), 3000); };
        const updateCartCount = () => { document.getElementById('cart-count').textContent = cartItems.reduce((sum, item) => sum + item.quantity, 0); };
        const addToCart = (product) => { const existingItem = cartItems.find(item => item.id === product.id && item.size === product.size); if (existingItem) { existingItem.quantity++; } else { cartItems.push({ ...product, quantity: 1 }); } updateCartCount(); showNotification(`${product.name} added to cart!`); };
        const changeQuantity = (productId, size, change) => { const item = cartItems.find(i => i.id === productId && i.size === size); if (item) { item.quantity += change; if (item.quantity <= 0) { removeFromCart(productId, size); } } updateCartCount(); renderCartPage(); };
        const removeFromCart = (productId, size) => { cartItems = cartItems.filter(item => !(item.id === productId && item.size === size)); updateCartCount(); renderCartPage(); };
        const placeOrder = async () => { const form = document.getElementById('checkout-form'); if (!form.checkValidity()) { form.reportValidity(); showNotification('Please fill all the required fields.', 'error'); return; } const placeOrderBtn = document.getElementById('place-order-btn'); placeOrderBtn.textContent = 'Placing Order...'; placeOrderBtn.disabled = true; let orderDetailsText = "Order Items:\n"; let subtotal = 0; cartItems.forEach(item => { orderDetailsText += `- ${item.name} (Size: ${item.size}) x ${item.quantity} = ₹${item.price * item.quantity}\n`; subtotal += item.price * item.quantity; }); orderDetailsText += `\nTotal Amount: ₹${subtotal.toFixed(2)}`; const formData = new FormData(form); formData.append('Order Summary', orderDetailsText); formData.append('Total Amount', `₹${subtotal.toFixed(2)}`); const formspreeEndpoint = 'https://formspree.io/f/mqalzbjy'; try { const response = await fetch(formspreeEndpoint, { method: 'POST', body: formData, headers: { 'Accept': 'application/json' } }); if (response.ok) { showPage('confirmation-page'); cartItems = []; updateCartCount(); form.reset(); } else { showNotification('Could not place order. Please try again.', 'error'); } } catch (error) { showNotification('Network error. Please check your connection.', 'error'); } finally { placeOrderBtn.textContent = 'Place Order'; placeOrderBtn.disabled = false; } };
        const renderOrderSummary = (containerId) => { const summaryContainer = document.getElementById(containerId); let subtotal = cartItems.reduce((sum, item) => sum + item.price * item.quantity, 0); summaryContainer.innerHTML = `<div class="bg-white p-6 rounded-lg shadow-md h-fit"><h2 class="text-xl font-bold mb-4 border-b pb-2">Order Summary</h2><div class="flex justify-between mb-2 text-gray-600"><span>Subtotal</span><span>₹${subtotal.toFixed(2)}</span></div><div class="flex justify-between mb-4 text-gray-600"><span>Shipping</span><span>FREE</span></div><div class="flex justify-between font-bold text-xl border-t pt-4"><span>Total</span><span>₹${subtotal.toFixed(2)}</span></div>${containerId === 'cart-summary' ? `<button id="proceed-to-checkout-btn" class="w-full bg-blue-500 text-white font-bold py-3 rounded-lg mt-6 hover:bg-blue-600 transition">Proceed to Checkout</button>` : `<button id="place-order-btn" class="w-full bg-green-500 text-white font-bold py-3 rounded-lg mt-6 hover:bg-green-600 transition">Place Order</button>`}</div>`; if (containerId === 'cart-summary') { document.getElementById('proceed-to-checkout-btn').addEventListener('click', () => { renderCheckoutPage(); showPage('checkout-page'); }); } else { document.getElementById('place-order-btn').addEventListener('click', placeOrder); } };
        const renderCartPage = () => { const cartContent = document.getElementById('cart-content'); if (cartItems.length === 0) { cartContent.innerHTML = `<div class="text-center py-16"><i class="fas fa-shopping-cart text-6xl text-gray-300 mb-4"></i><h2 class="text-2xl font-semibold text-gray-700 mb-2">Your cart is empty</h2><button class="nav-link bg-blue-500 text-white font-bold py-3 px-6 rounded-full hover:bg-blue-600 transition" data-page="home-page">Continue Shopping</button></div>`; cartContent.querySelector('.nav-link').addEventListener('click', () => showPage('home-page')); return; } cartContent.innerHTML = `<div class="flex flex-col lg:flex-row gap-8"><div id="cart-items-list" class="flex-grow"></div><div id="cart-summary" class="lg:w-1/3"></div></div>`; const cartItemsList = document.getElementById('cart-items-list'); cartItemsList.innerHTML = ''; cartItems.forEach(item => { const itemEl = document.createElement('div'); itemEl.className = 'flex items-center gap-4 bg-white p-4 rounded-lg shadow-sm mb-4'; itemEl.innerHTML = `<img src="${item.image}" alt="${item.name}" class="w-24 h-24 object-cover rounded-md"><div class="flex-grow"><h3 class="font-bold">${item.name}</h3><p class="text-sm text-gray-500">Size: ${item.size}</p><p class="font-semibold text-lg mt-1">₹${item.price}</p></div><div class="flex items-center gap-3"><button class="quantity-btn" onclick="cartApp.changeQuantity('${item.id}', '${item.size}', -1)">-</button><span class="font-bold w-8 text-center">${item.quantity}</span><button class="quantity-btn" onclick="cartApp.changeQuantity('${item.id}', '${item.size}', 1)">+</button></div><button class="text-red-500 hover:text-red-700" onclick="cartApp.removeFromCart('${item.id}', '${item.size}')"><i class="fas fa-trash-alt text-lg"></i></button>`; cartItemsList.appendChild(itemEl); }); renderOrderSummary('cart-summary'); };
        const renderCheckoutPage = () => { renderOrderSummary('checkout-summary'); };
        window.cartApp = { changeQuantity, removeFromCart };

        // --- SCROLL ANIMATION ---
        const animatedSections = document.querySelectorAll('.animated-section');
        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('is-visible');
                }
            });
        }, { threshold: 0.1 });
        animatedSections.forEach(section => observer.observe(section));

        // --- INITIALIZE APP ---
        const initApp = () => {
            renderAllProductsGrid();
            renderSubCategoryIcons();
            setupEventListeners();
            showPage('home-page');

            new Swiper('.swiper-container', {
                loop: true,
                autoplay: { delay: 3000, disableOnInteraction: false },
                pagination: { el: '.swiper-pagination', clickable: true },
                navigation: { nextEl: '.swiper-button-next', prevEl: '.swiper-button-prev' },
            });
        };

        initApp();
    });
    </script>
</body>
</html>
