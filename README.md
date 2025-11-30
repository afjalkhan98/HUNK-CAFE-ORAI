<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hunk Cafe - Flavorful Bites, Hookah Vibes & More</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Poppins', sans-serif; background-color: #f8f9fa; color: #333; }
        .hero { background: linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)), url('https://images.unsplash.com/photo-1414235077428-338989a2e8c0?ixlib=rb-4.0.3&auto=format&fit=crop&w=1920&q=80'); background-size: cover; background-position: center; height: 100vh; display: flex; align-items: center; justify-content: center; color: white; text-align: center; }
        .hero h1 { font-size: 3.5rem; font-weight: 700; text-shadow: 2px 2px 4px rgba(0,0,0,0.5); }
        .hero p { font-size: 1.2rem; font-weight: 300; text-shadow: 1px 1px 2px rgba(0,0,0,0.5); }
        .gallery { padding: 3rem 0; background: #fff; }
        .gallery img { height: 200px; object-fit: cover; border-radius: 10px; transition: transform 0.3s ease; loading: lazy; }
        .gallery img:hover { transform: scale(1.05); }
        .menu-section, .hookah-section { padding: 3rem 0; background: #f8f9fa; }
        .menu-card { background: white; border-radius: 15px; padding: 1.5rem; box-shadow: 0 5px 15px rgba(0,0,0,0.1); margin-bottom: 1rem; transition: box-shadow 0.3s ease; position: relative; }
        .menu-card:hover { box-shadow: 0 8px 25px rgba(0,0,0,0.15); }
        .menu-card img { width: 100%; height: 180px; object-fit: cover; border-radius: 10px; loading: lazy; }
        .price { font-size: 1.2rem; font-weight: 600; color: #28a745; }
        .add-to-cart { background: #ff6b35; color: white; border: none; padding: 10px 20px; border-radius: 25px; font-size: 0.9rem; transition: background 0.3s; }
        .add-to-cart:hover { background: #e55a2b; }
        .edit-section { display: none; margin-top: 10px; }
        .edit-section input { margin-bottom: 5px; width: 100%; padding: 5px; border-radius: 5px; border: 1px solid #ddd; }
        .edit-btn { display: none; background: #007bff; color: white; border: none; padding: 5px 10px; border-radius: 50%; font-size: 0.8rem; position: absolute; top: 10px; right: 10px; }
        .save-btn { background: #28a745; color: white; border: none; padding: 5px 10px; border-radius: 5px; margin-left: 5px; }
        .admin-mode .edit-btn { display: block; }
        .admin-mode .edit-section { display: block; }
        .admin-mode .location-edit { display: block; }
        .location-edit { display: none; margin-top: 15px; padding: 10px; background: #f0f8ff; border-radius: 10px; }
        .location-edit input, .location-edit textarea { margin-bottom: 10px; width: 100%; padding: 8px; border-radius: 5px; border: 1px solid #ddd; }
        .admin-login { position: fixed; top: 20px; right: 20px; z-index: 1050; }
        .admin-btn { background: #dc3545; color: white; border: none; padding: 10px 15px; border-radius: 25px; font-weight: 500; }
        .admin-mode .admin-btn { background: #28a745; }
        .modal-content { border-radius: 15px; }
        footer { background: linear-gradient(135deg, #ff6b35, #f7931e); color: white; padding: 2rem 0; text-align: center; font-weight: 300; }
        .navbar { background: linear-gradient(135deg, #ff6b35, #f7931e); box-shadow: 0 2px 10px rgba(255,107,53,0.3); }
        .navbar-brand { font-weight: 700; font-size: 1.5rem; }
        #map { height: 350px; border-radius: 10px; width: 100%; }
        .cart-total { font-weight: 600; color: #ff6b35; font-size: 1.2rem; }
        .toast-container { position: fixed; top: 20px; right: 20px; z-index: 1090; }
        .booking-section { padding: 3rem 0; background: #fff; }
        .btn { font-weight: 500; border-radius: 25px; padding: 10px 20px; }
        .change-pass-section { display: none; margin-top: 10px; }
        .admin-mode .change-pass-section { display: block; }
        .change-pass-section input { margin-bottom: 5px; width: 100%; padding: 5px; border-radius: 5px; border: 1px solid #ddd; }
        .options-section { padding: 3rem 0; background: #fff; }
        .option-card { text-align: center; margin-bottom: 1rem; }
        .option-card i { font-size: 3rem; color: #ff6b35; margin-bottom: 1rem; }
        @media (max-width: 768px) { 
            .hero h1 { font-size: 2.5rem; } 
            .hero p { font-size: 1rem; }
            #map { height: 250px; }
            .menu-card img { height: 150px; }
            .gallery img { height: 150px; }
            .navbar-brand { font-size: 1.2rem; }
            .add-to-cart { padding: 8px 16px; font-size: 0.8rem; width: 100%; margin-top: 5px; }
        }
        @media (max-width: 576px) { 
            .hero { height: 80vh; padding: 0 1rem; }
            section { padding: 2rem 1rem; }
        }
    </style>
</head>
<body>
    <!-- Navigation -->
    <nav class="navbar navbar-expand-lg navbar-dark">
        <div class="container">
            <a class="navbar-brand" href="#home"><i class="fas fa-utensils"></i> Hunk Cafe</a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav ms-auto">
                    <li class="nav-item"><a class="nav-link" href="#home">Home</a></li>
                    <li class="nav-item"><a class="nav-link" href="#options">Options</a></li>
                    <li class="nav-item"><a class="nav-link" href="#menu">Menu</a></li>
                    <li class="nav-item"><a class="nav-link" href="#hookah">Hookah</a></li>
                    <li class="nav-item"><a class="nav-link" href="#booking">Book Table</a></li>
                    <li class="nav-item"><a class="nav-link" href="#location">Location</a></li>
                    <li class="nav-item"><a class="nav-link" href="#cart" id="cartLink"><i class="fas fa-shopping-cart"></i> Cart (<span id="cartCount">0</span>)</a></li>
                </ul>
                <button class="btn admin-btn ms-3" data-bs-toggle="modal" data-bs-target="#adminModal"><i class="fas fa-user-shield"></i> <span id="adminText">Admin</span></button>
            </div>
        </div>
    </nav>

    <!-- Hero Section -->
    <section id="home" class="hero">
        <div>
            <h1>Welcome to Hunk Cafe</h1>
            <p>Savor authentic flavors, unwind with premium hookah, and book your spot in our vibrant lounge.</p>
            <a href="#options" class="btn btn-light btn-lg mt-3">Explore Options</a>
        </div>
    </section>

    <!-- New 3 Options Section -->
    <section id="options" class="options-section container">
        <h2 class="text-center mb-5 fw-light">Choose Your Experience</h2>
        <div class="row g-4">
            <div class="col-md-4">
                <div class="option-card">
                    <i class="fas fa-shopping-bag"></i>
                    <h4>Dine In</h4>
                    <p>Enjoy our cozy ambiance with fresh, hot meals served right to your table.</p>
                    <a href="#menu" class="btn btn-outline-warning">Start Ordering</a>
                </div>
            </div>
            <div class="col-md-4">
                <div class="option-card">
                    <i class="fas fa-motorcycle"></i>
                    <h4>Delivery</h4>
                    <p>Get your favorites delivered to your doorstep in under 30 minutes.</p>
                    <a href="#menu" class="btn btn-outline-warning">Order Delivery</a>
                </div>
            </div>
            <div class="col-md-4">
                <div class="option-card">
                    <i class="fas fa-calendar-alt"></i>
                    <h4>Takeaway</h4>
                    <p>Quick grab-and-go for busy days—pack your order and head out.</p>
                    <a href="#menu" class="btn btn-outline-warning">Quick Takeaway</a>
                </div>
            </div>
        </div>
    </section>

    <!-- Gallery Section -->
    <section class="gallery container">
        <h2 class="text-center mb-4 fw-light">A Glimpse of Deliciousness</h2>
        <div class="row g-3">
            <div class="col-md-3 col-sm-6"><img src="https://images.unsplash.com/photo-1513104890138-7c749659a591?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80" alt="Fresh Pizza" class="img-fluid w-100"></div>
            <div class="col-md-3 col-sm-6"><img src="https://images.unsplash.com/photo-1568901346375-23c9450c58cd?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80" alt="Juicy Burger" class="img-fluid w-100"></div>
            <div class="col-md-3 col-sm-6"><img src="https://images.unsplash.com/photo-1551028719-00167b16eac5?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80" alt="Decadent Sweets" class="img-fluid w-100"></div>
            <div class="col-md-3 col-sm-6"><img src="https://images.unsplash.com/photo-1578985545062-69928b1d9587?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80" alt="Steaming Maggi" class="img-fluid w-100"></div>
            <div class="col-md-3 col-sm-6"><img src="https://images.unsplash.com/photo-1553909488-df9a2d8dc26b?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80" alt="Crispy Sandwich" class="img-fluid w-100"></div>
            <div class="col-md-3 col-sm-6"><img src="https://images.unsplash.com/photo-1571934811376-b879e1d3213d?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80" alt="Refreshing Cold Drink" class="img-fluid w-100"></div>
            <div class="col-md-3 col-sm-6"><img src="https://images.unsplash.com/photo-1544551763-46a013bb70d5?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80" alt="Fresh Coconut Water" class="img-fluid w-100"></div>
            <div class="col-md-3 col-sm-6"><img src="https://images.unsplash.com/photo-1583337130417-3346a1be7dee?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80" alt="Exotic Hookah Setup" class="img-fluid w-100"></div>
        </div>
    </section>

    <!-- Menu Section -->
    <section id="menu" class="menu-section">
        <div class="container">
            <h2 class="text-center mb-5 fw-light">Menu - Order Online</h2>
            <div class="row" id="foodContainer">
                <div class="col-lg-6">
                    <h3 class="text-center mb-4 fw-semibold">Food Delights</h3>
                    <!-- Food items will be rendered here -->
                </div>
                <div class="col-lg-6">
                    <h3 class="text-center mb-4 fw-semibold">Refreshing Drinks</h3>
                    <!-- Drinks items will be rendered here -->
                </div>
            </div>
        </div>
    </section>

    <!-- Hookah Section -->
    <section id="hookah" class="hookah-section">
        <div class="container">
            <h2 class="text-center mb-5 fw-light">Premium Hookah Flavors</h2>
            <div class="row" id="hookahContainer">
                <!-- Hookah items will be rendered here -->
            </div>
        </div>
    </section>

    <!-- Booking Section -->
    <section id="booking" class="booking-section">
        <div class="container">
            <h2 class="text-center mb-5 fw-light">Book a Table</h2>
            <form id="bookingForm">
                <div class="row g-3">
                    <div class="col-md-6"><input type="text" class="form-control" id="bookName" placeholder="Your Name" required></div>
                    <div class="col-md-6"><input type="email" class="form-control" id="bookEmail" placeholder="Your Email" required></div>
                    <div class="col-md-4"><input type="date" class="form-control" id="bookDate" required></div>
                    <div class="col-md-4"><input type="time" class="form-control" id="bookTime" required></div>
                    <div class="col-md-4"><input type="number" class="form-control" id="bookGuests" placeholder="Number of Guests" min="1" required></div>
                    <div class="col-12"><textarea class="form-control" id="bookRequests" rows="3" placeholder="Special Requests"></textarea></div>
                    <div class="col-12"><button type="submit" class="btn btn-warning w-100">Book Now</button></div>
                </div>
            </form>
        </div>
    </section>

    <!-- Location Section -->
    <section id="location" class="py-5 bg-light">
        <div class="container">
            <h2 class="text-center mb-5 fw-light">Our Location</h2>
            <div class="row">
                <div class="col-md-6">
                    <div id="locationDetails">
                        <p class="fw-medium" id="address"><i class="fas fa-map-marker-alt me-2"></i> 4th Floor, Ganesh Plaza, Ajit Mill Cross Road, Rakhial, Ahmedabad</p>
                        <p id="phone"><i class="fas fa-phone me-2"></i> +91 98987 02437</p>
                        <p id="email"><i class="fas fa-envelope me-2"></i> info@hunkcafe.com</p>
                        <p id="hours">Hours: 9AM - 12AM Daily</p>
                    </div>
                    <div class="location-edit">
                        <h5>Edit Location Details</h5>
                        <textarea id="edit-address" placeholder="Address" rows="2"></textarea>
                        <input type="tel" id="edit-phone" placeholder="Phone">
                        <input type="email" id="edit-email" placeholder="Email">
                        <textarea id="edit-hours" placeholder="Hours" rows="1"></textarea>
                        <button class="btn btn-primary save-btn" onclick="saveLocationEdit()">Save Changes</button>
                    </div>
                    <a href="https://maps.app.goo.gl/6CvnyGkMLQQwcg6Q8" target="_blank" class="btn btn-primary mt-2">Get Directions</a>
                </div>
                <div class="col-md-6">
                    <iframe id="map" src="https://www.google.com/maps/embed/v1/place?q=4th+Floor%2C+Ganesh+Plaza%2C+Ajit+Mill+Cross+Road%2C+Rakhial%2C+Ahmedabad&key=" allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade"></iframe>
                </div>
            </div>
        </div>
    </section>

    <!-- Cart Modal -->
    <div class="modal fade" id="cartModal" tabindex="-1">
        <div class="modal-dialog modal-lg">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">Your Cart</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
                </div>
                <div class="modal-body">
                    <div id="cartItems"></div>
                    <hr>
                    <p class="cart-total text-end mb-0">Total: ₹<span id="cartTotal">0</span></p>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
                    <button type="button" class="btn btn-success" onclick="placeOrder()">Place Order</button>
                </div>
            </div>
        </div>
    </div>

    <!-- Admin Login Modal -->
    <div class="modal fade" id="adminModal" tabindex="-1">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">Admin Login</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
                </div>
                <div class="modal-body">
                    <form id="adminForm">
                        <div class="mb-3"><input type="text" class="form-control" id="username" placeholder="Username" required></div>
                        <div class="mb-3"><input type="password" class="form-control" id="password" placeholder="Password" required></div>
                        <button type="submit" class="btn btn-primary w-100">Login</button>
                    </form>
                    <div class="change-pass-section" id="changePassSection">
                        <h6>Change Password</h6>
                        <input type="password" id="new-password" placeholder="New Password">
                        <input type="password" id="confirm-password" placeholder="Confirm New Password">
                        <button class="btn btn-secondary w-100 mt-2" onclick="changePassword()">Update Password</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Toast Notification -->
    <div class="toast-container">
        <div id="orderToast" class="toast align-items-center text-white bg-success border-0" role="alert">
            <div class="d-flex">
                <div class="toast-body"><i class="fas fa-check me-2"></i>Your order has been received. We'll prepare it fresh!</div>
                <button type="button" class="btn-close btn-close-white me-2 m-auto" data-bs-dismiss="toast"></button>
            </div>
        </div>
        <div id="bookingToast" class="toast align-items-center text-white bg-info border-0" role="alert">
            <div class="d-flex">
                <div class="toast-body"><i class="fas fa-calendar-check me-2"></i>Table booked successfully! We'll confirm via email.</div>
                <button type="button" class="btn-close btn-close-white me-2 m-auto" data-bs-dismiss="toast"></button>
            </div>
        </div>
    </div>

    <footer>
        <div class="container">
            <p>&copy; 2025 Hunk Cafe. All rights reserved. | Crafted with <i class="fas fa-heart" style="color: #ffcccb;"></i> for epic foodies.</p>
        </div>
    </footer>

    <!-- EmailJS Script - Replace with your IDs -->
    <script type="text/javascript" src="https://cdn.jsdelivr.net/npm/@emailjs/browser@4/dist/email.min.js"></script>
    <script type="text/javascript">
        // Initialize EmailJS - REPLACE THESE WITH YOUR IDs
        emailjs.init("1DFHqP53utvFr3vHW");
        const SERVICE_ID = "YOUR_SERVICE_ID"; // e.g., "service_def456"
        const ORDER_TEMPLATE_ID = "YOUR_ORDER_TEMPLATE_ID"; // e.g., "template_ghi789"
        const BOOKING_TEMPLATE_ID = "YOUR_BOOKING_TEMPLATE_ID"; // e.g., "template_jkl012"
    </script>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
    <script>
        // Site Data
        let siteData = JSON.parse(localStorage.getItem('siteData')) || {
            location: {
                address: '4th Floor, Ganesh Plaza, Ajit Mill Cross Road, Rakhial, Ahmedabad',
                phone: '+91 98987 02437',
                email: 'info@hunkcafe.com',
                hours: 'Hours: 9AM - 12AM Daily'
            },
            adminPassword: 'hunk123' // Default password
        };

        // Menu Data
        let menuData = JSON.parse(localStorage.getItem('menuData')) || {
            food: [
                { id: 1, name: 'Margherita Pizza', price: 199, img: 'https://images.unsplash.com/photo-1513104890138-7c749659a591?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80' },
                { id: 2, name: 'Classic Burger', price: 149, img: 'https://images.unsplash.com/photo-1568901346375-23c9450c58cd?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80' },
                { id: 3, name: 'Chocolate Brownie', price: 89, img: 'https://images.unsplash.com/photo-1551028719-00167b16eac5?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80' },
                { id: 4, name: 'Spicy Maggi', price: 69, img: 'https://images.unsplash.com/photo-1578985545062-69928b1d9587?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80' },
                { id: 5, name: 'Grilled Cheese Sandwich', price: 109, img: 'https://images.unsplash.com/photo-1553909488-df9a2d8dc26b?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80' }
            ],
            drinks: [
                { id: 6, name: 'Chilled Cola', price: 49, img: 'https://images.unsplash.com/photo-1571934811376-b879e1d3213d?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80' },
                { id: 7, name: 'Fresh Coconut Water', price: 59, img: 'https://images.unsplash.com/photo-1544551763-46a013bb70d5?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80' }
            ],
            hookah: [
                { id: 8, name: 'Paan', price: 299, img: 'https://images.unsplash.com/photo-1583337130417-3346a1be7dee?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80' },
                { id: 9, name: 'Mint', price: 249, img: 'https://images.unsplash.com/photo-1583337130417-3346a1be7dee?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80' },
                { id: 10, name: 'Dubai Mix', price: 349, img: 'https://images.unsplash.com/photo-1583337130417-3346a1be7dee?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80' },
                { id: 11, name: 'Magai Paan', price: 299, img: 'https://images.unsplash.com/photo-1583337130417-3346a1be7dee?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80' }
            ]
        };

        let cart = JSON.parse(localStorage.getItem('cart')) || [];
        let isAdmin = sessionStorage.getItem('isAdmin') === 'true';

        // Render Functions
        function renderMenu() {
            const foodContainer = document.querySelector('#foodContainer .col-lg-6:first-child');
            foodContainer.innerHTML = '<h3 class="text-center mb-4 fw-semibold">Food Delights</h3>' + menuData.food.map(item => createMenuCard(item, 'food')).join('');

            const drinksContainer = document.querySelector('#foodContainer .col-lg-6:last-child');
            drinksContainer.innerHTML = '<h3 class="text-center mb-4 fw-semibold">Refreshing Drinks</h3>' + menuData.drinks.map(item => createMenuCard(item, 'drinks')).join('');

            const hookahContainer = document.getElementById('hookahContainer');
            hookahContainer.innerHTML = menuData.hookah.map(item => createMenuCard(item, 'hookah', true)).join('');
        }

        function createMenuCard(item, category, center = false) {
            const colClass = center ? 'col-md-3' : 'col-12';
            const align = center ? 'text-center' : '';
            return `
                <div class="${colClass}">
                    <div class="menu-card ${align}">
                        <button class="edit-btn            <div class="col-md-3 col-sm-6"><img src="https://images.unsplash.com/photo-1578985545062-69928b1d9587?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80" alt="Steaming Maggi" class="img-fluid w-100"></div>
            <div class="col-md-3 col-sm-6"><img src="https://images.unsplash.com/photo-1553909488-df9a2d8dc26b?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80" alt="Crispy Sandwich" class="img-fluid w-100"></div>
            <div class="col-md-3 col-sm-6"><img src="https://images.unsplash.com/photo-1571934811376-b879e1d3213d?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80" alt="Refreshing Cold Drink" class="img-fluid w-100"></div>
            <div class="col-md-3 col-sm-6"><img src="https://images.unsplash.com/photo-1544551763-46a013bb70d5?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80" alt="Fresh Coconut Water" class="img-fluid w-100"></div>
            <div class="col-md-3 col-sm-6"><img src="https://images.unsplash.com/photo-1583337130417-3346a1be7dee?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80" alt="Exotic Hookah Setup" class="img-fluid w-100"></div>
        </div>
    </section>

    <!-- Menu Section -->
    <section id="menu" class="menu-section">
        <div class="container">
            <h2 class="text-center mb-5 fw-light">Menu - Order Online</h2>
            <div class="row" id="foodContainer">
                <div class="col-lg-6">
                    <h3 class="text-center mb-4 fw-semibold">Food Delights</h3>
                    <!-- Food items will be rendered here -->
                </div>
                <div class="col-lg-6">
                    <h3 class="text-center mb-4 fw-semibold">Refreshing Drinks</h3>
                    <!-- Drinks items will be rendered here -->
                </div>
            </div>
        </div>
    </section>

    <!-- Hookah Section -->
    <section id="hookah" class="hookah-section">
        <div class="container">
            <h2 class="text-center mb-5 fw-light">Premium Hookah Flavors</h2>
            <div class="row" id="hookahContainer">
                <!-- Hookah items will be rendered here -->
            </div>
        </div>
    </section>

    <!-- Booking Section -->
    <section id="booking" class="booking-section">
        <div class="container">
            <h2 class="text-center mb-5 fw-light">Book a Table</h2>
            <form id="bookingForm">
                <div class="row g-3">
                    <div class="col-md-6"><input type="text" class="form-control" placeholder="Your Name" required></div>
                    <div class="col-md-6"><input type="email" class="form-control" placeholder="Your Email" required></div>
                    <div class="col-md-4"><input type="date" class="form-control" required></div>
                    <div class="col-md-4"><input type="time" class="form-control" required></div>
                    <div class="col-md-4"><input type="number" class="form-control" placeholder="Number of Guests" min="1" required></div>
                    <div class="col-12"><textarea class="form-control" rows="3" placeholder="Special Requests"></textarea></div>
                    <div class="col-12"><button type="submit" class="btn btn-warning w-100">Book Now</button></div>
                </div>
            </form>
        </div>
    </section>

    <!-- Location Section -->
    <section id="location" class="py-5 bg-light">
        <div class="container">
            <h2 class="text-center mb-5 fw-light">Our Location</h2>
            <div class="row">
                <div class="col-md-6">
                    <div id="locationDetails">
                        <p class="fw-medium" id="address"><i class="fas fa-map-marker-alt me-2"></i> 4th Floor, Ganesh Plaza, Ajit Mill Cross Road, Rakhial, Ahmedabad</p>
                        <p id="phone"><i class="fas fa-phone me-2"></i> +91 98987 02437</p>
                        <p id="email"><i class="fas fa-envelope me-2"></i> info@hunkcafe.com</p>
                        <p id="hours">Hours: 9AM - 12AM Daily</p>
                    </div>
                    <div class="location-edit">
                        <h5>Edit Location Details</h5>
                        <textarea id="edit-address" placeholder="Address" rows="2"></textarea>
                        <input type="tel" id="edit-phone" placeholder="Phone">
                        <input type="email" id="edit-email" placeholder="Email">
                        <textarea id="edit-hours" placeholder="Hours" rows="1"></textarea>
                        <button class="btn btn-primary save-btn" onclick="saveLocationEdit()">Save Changes</button>
                    </div>
                    <a href="https://maps.app.goo.gl/6CvnyGkMLQQwcg6Q8" target="_blank" class="btn btn-primary mt-2">Get Directions</a>
                </div>
                <div class="col-md-6">
                    <iframe id="map" src="https://www.google.com/maps/embed/v1/place?q=4th+Floor%2C+Ganesh+Plaza%2C+Ajit+Mill+Cross+Road%2C+Rakhial%2C+Ahmedabad&key=" allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade"></iframe>
                </div>
            </div>
        </div>
    </section>

    <!-- Cart Modal -->
    <div class="modal fade" id="cartModal" tabindex="-1">
        <div class="modal-dialog modal-lg">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">Your Cart</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
                </div>
                <div class="modal-body">
                    <div id="cartItems"></div>
                    <hr>
                    <p class="cart-total text-end mb-0">Total: ₹<span id="cartTotal">0</span></p>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
                    <button type="button" class="btn btn-success" onclick="placeOrder()">Place Order</button>
                </div>
            </div>
        </div>
    </div>

    <!-- Admin Login Modal -->
    <div class="modal fade" id="adminModal" tabindex="-1">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">Admin Login</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
                </div>
                <div class="modal-body">
                    <form id="adminForm">
                        <div class="mb-3"><input type="text" class="form-control" id="username" placeholder="Username" required></div>
                        <div class="mb-3"><input type="password" class="form-control" id="password" placeholder="Password" required></div>
                        <button type="submit" class="btn btn-primary w-100">Login</button>
                    </form>
                    <div class="change-pass-section" id="changePassSection">
                        <h6>Change Password</h6>
                        <input type="password" id="new-password" placeholder="New Password">
                        <input type="password" id="confirm-password" placeholder="Confirm New Password">
                        <button class="btn btn-secondary w-100 mt-2" onclick="changePassword()">Update Password</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Toast Notification -->
    <div class="toast-container">
        <div id="orderToast" class="toast align-items-center text-white bg-success border-0" role="alert">
            <div class="d-flex">
                <div class="toast-body"><i class="fas fa-check me-2"></i>Your order has been received. We'll prepare it fresh!</div>
                <button type="button" class="btn-close btn-close-white me-2 m-auto" data-bs-dismiss="toast"></button>
            </div>
        </div>
        <div id="bookingToast" class="toast align-items-center text-white bg-info border-0" role="alert">
            <div class="d-flex">
                <div class="toast-body"><i class="fas fa-calendar-check me-2"></i>Table booked successfully! We'll confirm via email.</div>
                <button type="button" class="btn-close btn-close-white me-2 m-auto" data-bs-dismiss="toast"></button>
            </div>
        </div>
    </div>

    <footer>
        <div class="container">
            <p>&copy; 2025 Hunk Cafe. All rights reserved. | Crafted with <i class="fas fa-heart" style="color: #ffcccb;"></i> for epic foodies.</p>
        </div>
    </footer>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
    <script>
        // Site Data
        let siteData = JSON.parse(localStorage.getItem('siteData')) || {
            location: {
                address: '4th Floor, Ganesh Plaza, Ajit Mill Cross Road, Rakhial, Ahmedabad',
                phone: '+91 98987 02437',
                email: 'info@hunkcafe.com',
                hours: 'Hours: 9AM - 12AM Daily'
            },
            adminPassword: 'hunk123' // Default password
        };

        // Menu Data
        let menuData = JSON.parse(localStorage.getItem('menuData')) || {
            food: [
                { id: 1, name: 'Margherita Pizza', price: 199, img: 'https://images.unsplash.com/photo-1513104890138-7c749659a591?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80' },
                { id: 2, name: 'Classic Burger', price: 149, img: 'https://images.unsplash.com/photo-1568901346375-23c9450c58cd?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80' },
                { id: 3, name: 'Chocolate Brownie', price: 89, img: 'https://images.unsplash.com/photo-1551028719-00167b16eac5?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80' },
                { id: 4, name: 'Spicy Maggi', price: 69, img: 'https://images.unsplash.com/photo-1578985545062-69928b1d9587?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80' },
                { id: 5, name: 'Grilled Cheese Sandwich', price: 109, img: 'https://images.unsplash.com/photo-1553909488-df9a2d8dc26b?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80' }
            ],
            drinks: [
                { id: 6, name: 'Chilled Cola', price: 49, img: 'https://images.unsplash.com/photo-1571934811376-b879e1d3213d?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80' },
                { id: 7, name: 'Fresh Coconut Water', price: 59, img: 'https://images.unsplash.com/photo-1544551763-46a013bb70d5?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80' }
            ],
            hookah: [
                { id: 8, name: 'Paan', price: 299, img: 'https://images.unsplash.com/photo-1583337130417-3346a1be7dee?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80' },
                { id: 9, name: 'Mint', price: 249, img: 'https://images.unsplash.com/photo-1583337130417-3346a1be7dee?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80' },
                { id: 10, name: 'Dubai Mix', price: 349, img: 'https://images.unsplash.com/photo-1583337130417-3346a1be7dee?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80' },
                { id: 11, name: 'Magai Paan', price: 299, img: 'https://images.unsplash.com/photo-1583337130417-3346a1be7dee?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80' }
            ]
        };

        let cart = JSON.parse(localStorage.getItem('cart')) || [];
        let isAdmin = sessionStorage.getItem('isAdmin') === 'true';

        // Render Functions
        function renderMenu() {
            const foodContainer = document.querySelector('#foodContainer .col-lg-6:first-child');
            foodContainer.innerHTML = '<h3 class="text-center mb-4 fw-semibold">Food Delights</h3>' + menuData.food.map(item => createMenuCard(item, 'food')).join('');

            const drinksContainer = document.querySelector('#foodContainer .col-lg-6:last-child');
            drinksContainer.innerHTML = '<h3 class="text-center mb-4 fw-semibold">Refreshing Drinks</h3>' + menuData.drinks.map(item => createMenuCard(item, 'drinks')).join('');

            const hookahContainer = document.getElementById('hookahContainer');
            hookahContainer.innerHTML = menuData.hookah.map(item => createMenuCard(item, 'hookah', true)).join('');
        }

        function createMenuCard(item, category, center = false) {
            const colClass = center ? 'col-md-3' : 'col-12';
            const align = center ? 'text-center' : '';
            return `
                <div class="${colClass}">
                    <div class="menu-card ${align}">
                        <button class="edit-btn" onclick="toggleEdit(${item.id})" title="Edit"><i class="fas fa-edit"></i></button>
                        <img src="${item.img}" alt="${item.name}" onerror="this.src='https://via.placeholder.com/300x200?text=${encodeURIComponent(item.name)}'">
                        <h5 class="mt-3">${item.name}</h5>
                        <p class="price">₹${item.price}</p>
                        <button class="add-to-cart" onclick="addToCart('${item.name}', ${item.price})">Add to Cart</button>
                        <div class="edit-section" id="edit-${item.id}">
                            <input type="number" id="price-${item.id}" value="${item.price}" placeholder="New Price" min="0">
                            <input type="url" id="img-${item.id}" value="${item.img}" placeholder="New Image URL">
                            <button class="save-btn" onclick="saveEdit(${item.id}, '${category}')">Save</button>
                        </div>
                    </div>
                </div>
            `;
        }

        function toggleEdit(id) {
            if (!isAdmin) return; // Extra safety
            const editSection = document.getElementById(`edit-${id}`);
            editSection.style.display = editSection.style.display === 'block' ? 'none' : 'block';
        }

        function saveEdit(id, category) {
            if (!isAdmin) return;
            const item = [...menuData.food, ...menuData.drinks, ...menuData.hookah].find(i => i.id === id);
            if (item) {
                item.price = parseInt(document.getElementById(`price-${id}`).value) || item.price;
                item.img = document.getElementById(`img-${id}`).value || item.img;
                localStorage.setItem('menuData', JSON.stringify(menuData));
                renderMenu(); // Re-render to update
                alert('Item updated successfully!');
            }
        }

        // Location Render & Edit
        function renderLocation() {
            document.getElementById('address').innerHTML = `<i class="fas fa-map-marker-alt me-2"></i> ${siteData.location.address}`;
            document.getElementById('phone').innerHTML = `<i class="fas fa-phone me-2"></i> ${siteData.location.phone}`;
            document.getElementById('email').innerHTML = `<i class="fas fa-envelope me-2"></i> ${siteData.location.email}`;
            document.getElementById('hours').innerHTML = siteData.location.hours;

            // Populate edit fields
            document.getElementById('edit-address').value = siteData.location.address;
            document.getElementById('edit-phone').value = siteData.location.phone;
            document.getElementById('edit-email').value = siteData.location.email;
            document.getElementById('edit-hours').value = siteData.location.hours;
        }

        function saveLocationEdit() {
            if (!isAdmin) return;
            siteData.location.address = document.getElementById('edit-address').value || siteData.location.address;
            siteData.location.phone = document.getElementById('edit-phone').value || siteData.location.phone;
            siteData.location.email = document.getElementById('edit-email').value || siteData.location.email;
            siteData.location.hours = document.getElementById('edit-hours').value || siteData.location.hours;
            localStorage.setItem('siteData', JSON.stringify(siteData));
            renderLocation();
            alert('Location details updated!');
        }

        // Password Change
        function changePassword() {
            if (!isAdmin) return;
            const newPass = document.getElementById('new-password').value;
            const confirmPass = document.getElementById('confirm-password').value;
            if (newPass && newPass === confirmPass) {
                siteData.adminPassword = newPass;
                localStorage.setItem('siteData', JSON.stringify(siteData));
                alert('Password updated successfully!');
                document.getElementById('new-password').value = '';
                document.getElementById('confirm-password').value = '';
            } else {
                alert('Passwords do not match or empty!');
            }
        }

        // Cart Functions
        function addToCart(name, price) {
            cart.push({ name, price });
            localStorage.setItem('cart', JSON.stringify(cart));
            updateCartCount();
            const toast = new bootstrap.Toast(document.getElementById('orderToast'));
            toast.show();
        }

        function updateCartCount() {
            document.getElementById('cartCount').textContent = cart.length;
        }

        function displayCart() {
            const cartItems = document.getElementById('cartItems');
            const total = cart.reduce((sum, item) => sum + item.price, 0);
            cartItems.innerHTML = cart.map((item, idx) => `<div class="d-flex justify-content-between"><span>${item.name}</span><span>₹${item.price}</span><button class="btn btn-sm btn-danger ms-2" onclick="removeFromCart(${idx})">Remove</button></div>`).join('') || '<p>Your cart is empty.</p>';
            document.getElementById('cartTotal').textContent = total;
        }

        function removeFromCart(idx) {
            cart.splice(idx, 1);
            localStorage.setItem('cart', JSON.stringify(cart));
            updateCartCount();
            displayCart();
        }

        function placeOrder() {
            if (cart.length === 0) return alert('Cart is empty!');
            localStorage.removeItem('cart');
            cart = [];
            updateCartCount();
            const toast = new bootstrap.Toast(document.getElementById('orderToast'));
            toast.show();
            bootstrap.Modal.getInstance(document.getElementById('cartModal')).hide();
        }

        // Admin Login
        document.getElementById('adminForm').addEventListener('submit', function(e) {
            e.preventDefault();
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            if (username === 'admin' && password === siteData.adminPassword) {
                isAdmin = true;
                sessionStorage.setItem('isAdmin', 'true');
                document.body.classList.add('admin-mode');
                document.getElementById('adminText').textContent = 'Logout';
                document.getElementById('changePassSection').style.display = 'block';
                bootstrap.Modal.getInstance(document.getElementById('adminModal')).hide();
                alert('Admin mode activated! Edit options now visible.');
            } else {
                alert('Invalid credentials!');
            }
        });

        // Admin Button (Login/Logout)
        document.querySelector('.admin-btn').addEventListener('click', function(e) {
            if (isAdmin) {
                e.preventDefault();
                e.stopPropagation();
                isAdmin = false;
                sessionStorage.removeItem('isAdmin');
                document.body.classList.remove('admin-mode');
                document.getElementById('adminText').textContent = 'Admin';
                document.getElementById('changePassSection').style.display = 'none';
                alert('Logged out.');
            }
        });

        // Booking Form
        document.getElementById('bookingForm').addEventListener('submit', function(e) {
            e.preventDefault();
            const bookingToast = new bootstrap.Toast(document.getElementById('bookingToast'));
            bookingToast.show();
            this.reset();
        });

        // Cart Modal Trigger
        document.getElementById('cartLink').addEventListener('click', function(e) {
            e.preventDefault();
            displayCart();
            new bootstrap.Modal(document.getElementById('cartModal')).show();
        });

        // Smooth Scrolling
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                document.querySelector(this.getAttribute('href')).scrollIntoView({ behavior: 'smooth' });
            });
        });

        // Initialize
        if (isAdmin) {
            document.body.classList.add('admin-mode');
            document.getElementById('adminText').textContent = 'Logout';
            document.getElementById('changePassSection').style.display = 'block';
        }
        renderMenu();
        renderLocation();
        updateCartCount();
    </script>
</body>
</html>
