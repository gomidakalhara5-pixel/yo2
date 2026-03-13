<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Campus Lost & Found</title>
    <!-- Bootstrap 5 CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <!-- FontAwesome -->
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --primary-color: #0d2c54; /* University Navy */
            --secondary-color: #f7c948; /* Campus Gold */
            --accent-color: #e63946;
            --light-bg: #f8f9fa;
            --text-dark: #333;
            --card-hover-transform: translateY(-5px);
            --transition-speed: 0.3s;
        }

        body {
            font-family: 'Poppins', sans-serif;
            background-color: var(--light-bg);
            color: var(--text-dark);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }

        /* Navigation */
        .navbar {
            background-color: var(--primary-color);
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        .navbar-brand {
            font-weight: 700;
            color: white !important;
            font-size: 1.5rem;
        }
        .navbar-brand i {
            color: var(--secondary-color);
        }
        .nav-link {
            color: rgba(255,255,255,0.8) !important;
            font-weight: 500;
            transition: var(--transition-speed);
        }
        .nav-link:hover, .nav-link.active {
            color: white !important;
            transform: scale(1.05);
        }

        /* Sections */
        .page-section {
            display: none; /* Hidden by default, toggled by JS */
            padding: 2rem 0;
            animation: fadeIn 0.5s ease-in-out;
        }
        .page-section.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Hero Section */
        .hero-section {
            background: linear-gradient(rgba(13, 44, 84, 0.9), rgba(13, 44, 84, 0.8)), url('https://images.unsplash.com/photo-1541339907198-e08756dedf3f?ixlib=rb-1.2.1&auto=format&fit=crop&w=1950&q=80');
            background-size: cover;
            background-position: center;
            color: white;
            padding: 100px 0;
            text-align: center;
            border-radius: 0 0 50px 50px;
            margin-bottom: 2rem;
        }
        .hero-btn {
            padding: 12px 30px;
            font-weight: 600;
            border-radius: 30px;
            transition: var(--transition-speed);
            margin: 10px;
        }
        .btn-lost {
            background-color: var(--accent-color);
            border: none;
            color: white;
        }
        .btn-lost:hover { background-color: #c92a37; color: white; transform: scale(1.05); }
        .btn-found {
            background-color: var(--secondary-color);
            border: none;
            color: var(--primary-color);
        }
        .btn-found:hover { background-color: #e0b12d; color: var(--primary-color); transform: scale(1.05); }

        /* Cards */
        .item-card {
            border: none;
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 5px 15px rgba(0,0,0,0.05);
            transition: var(--transition-speed);
            background: white;
            height: 100%;
        }
        .item-card:hover {
            transform: var(--card-hover-transform);
            box-shadow: 0 15px 30px rgba(0,0,0,0.1);
        }
        .card-img-top {
            height: 200px;
            object-fit: cover;
            background-color: #eee;
        }
        .badge-lost { background-color: var(--accent-color); }
        .badge-found { background-color: var(--secondary-color); color: var(--primary-color); }
        
        .card-footer {
            background: white;
            border-top: 1px solid #f1f1f1;
        }

        /* Forms */
        .form-container {
            background: white;
            padding: 2rem;
            border-radius: 15px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.05);
        }
        .form-control:focus {
            border-color: var(--primary-color);
            box-shadow: 0 0 0 0.25rem rgba(13, 44, 84, 0.25);
        }

        /* Stats */
        .stat-card {
            background: white;
            border-radius: 15px;
            padding: 1.5rem;
            text-align: center;
            box-shadow: 0 5px 15px rgba(0,0,0,0.05);
            border-bottom: 4px solid var(--primary-color);
        }
        .stat-icon {
            font-size: 2.5rem;
            color: var(--primary-color);
            margin-bottom: 1rem;
        }
        .stat-number {
            font-size: 2rem;
            font-weight: 700;
            color: var(--text-dark);
        }

        /* Footer */
        footer {
            background-color: var(--primary-color);
            color: white;
            margin-top: auto;
            padding: 2rem 0;
        }
        .social-icons a {
            color: white;
            margin: 0 10px;
            font-size: 1.2rem;
            transition: 0.3s;
        }
        .social-icons a:hover { color: var(--secondary-color); }

        /* Utilities */
        .text-primary-custom { color: var(--primary-color); }
        .bg-gradient-custom { background: linear-gradient(135deg, var(--primary-color), #1a4a8a); }
        
        /* Floating Action Button for Mobile */
        .fab {
            position: fixed;
            bottom: 30px;
            right: 30px;
            width: 60px;
            height: 60px;
            background-color: var(--secondary-color);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 4px 10px rgba(0,0,0,0.3);
            cursor: pointer;
            z-index: 1000;
            transition: 0.3s;
            display: none; /* Shown on mobile via media query if needed, or JS */
        }
        .fab:hover { transform: scale(1.1); }
        .fab i { font-size: 24px; color: var(--primary-color); }

        /* Toast Notification */
        .toast-container { position: fixed; top: 20px; right: 20px; z-index: 9999; }
    </style>
</head>
<body>

    <!-- Navbar -->
    <nav class="navbar navbar-expand-lg navbar-dark sticky-top">
        <div class="container">
            <a class="navbar-brand" href="#" onclick="app.showPage('home')">
                <i class="fas fa-university me-2"></i>Campus<span style="color: var(--secondary-color);">Finder</span>
            </a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav ms-auto">
                    <li class="nav-item"><a class="nav-link active" href="#" onclick="app.showPage('home')">Home</a></li>
                    <li class="nav-item"><a class="nav-link" href="#" onclick="app.showPage('browse')">Browse Items</a></li>
                    <li class="nav-item"><a class="nav-link" href="#" onclick="app.showPage('report')">Report Item</a></li>
                    <li class="nav-item"><a class="nav-link" href="#" onclick="app.showPage('admin')">Dashboard</a></li>
                    <li class="nav-item"><a class="nav-link" href="#" onclick="app.showPage('contact')">Contact</a></li>
                </ul>
            </div>
        </div>
    </nav>

    <!-- Notification Toast -->
    <div class="toast-container">
        <div id="liveToast" class="toast align-items-center text-white bg-success border-0" role="alert" aria-live="assertive" aria-atomic="true">
            <div class="d-flex">
                <div class="toast-body" id="toastMessage">
                    Action successful!
                </div>
                <button type="button" class="btn-close btn-close-white me-2 m-auto" data-bs-dismiss="toast" aria-label="Close"></button>
            </div>
        </div>
    </div>

    <!-- HOME PAGE -->
    <section id="home" class="page-section active">
        <div class="hero-section">
            <div class="container">
                <h1 class="display-4 fw-bold mb-3">Lost Something? Found Something?</h1>
                <p class="lead mb-4">The official central hub for lost and found items on campus.</p>
                <div class="d-flex justify-content-center flex-wrap">
                    <button class="btn btn-lost hero-btn" onclick="app.prefillReport('lost')">
                        <i class="fas fa-search me-2"></i>I Lost Something
                    </button>
                    <button class="btn btn-found hero-btn" onclick="app.prefillReport('found')">
                        <i class="fas fa-hand-holding-heart me-2"></i>I Found Something
                    </button>
                </div>
            </div>
        </div>

        <div class="container">
            <div class="row g-4 mb-5">
                <div class="col-md-4">
                    <div class="stat-card">
                        <div class="stat-icon"><i class="fas fa-box-open"></i></div>
                        <div class="stat-number" id="totalItemsCount">0</div>
                        <div class="text-muted">Total Items Reported</div>
                    </div>
                </div>
                <div class="col-md-4">
                    <div class="stat-card">
                        <div class="stat-icon" style="color: var(--accent-color);"><i class="fas fa-search-location"></i></div>
                        <div class="stat-number" id="lostItemsCount">0</div>
                        <div class="text-muted">Items Currently Lost</div>
                    </div>
                </div>
                <div class="col-md-4">
                    <div class="stat-card">
                        <div class="stat-icon" style="color: var(--secondary-color);"><i class="fas fa-check-circle"></i></div>
                        <div class="stat-number" id="foundItemsCount">0</div>
                        <div class="text-muted">Items Found & Returned</div>
                    </div>
                </div>
            </div>

            <h3 class="mb-4 border-bottom pb-2">Recent Listings</h3>
            <div class="row g-4" id="recentItemsContainer">
                <!-- Dynamically populated -->
            </div>
            <div class="text-center mt-4">
                <button class="btn btn-outline-primary rounded-pill" onclick="app.showPage('browse')">View All Items</button>
            </div>
        </div>
    </section>

    <!-- BROWSE PAGE -->
    <section id="browse" class="page-section">
        <div class="container">
            <h2 class="mb-4 fw-bold text-primary-custom">Browse Items</h2>
            
            <!-- Filters -->
            <div class="card p-3 mb-4 border-0 shadow-sm">
                <div class="row g-3">
                    <div class="col-md-4">
                        <div class="input-group">
                            <span class="input-group-text bg-white border-end-0"><i class="fas fa-search text-muted"></i></span>
                            <input type="text" class="form-control border-start-0" id="searchInput" placeholder="Search items..." onkeyup="app.filterItems()">
                        </div>
                    </div>
                    <div class="col-md-3">
                        <select class="form-select" id="categoryFilter" onchange="app.filterItems()">
                            <option value="">All Categories</option>
                            <option value="Electronics">Electronics</option>
                            <option value="Books">Books</option>
                            <option value="ID Cards">ID Cards</option>
                            <option value="Bags">Bags</option>
                            <option value="Clothing">Clothing</option>
                            <option value="Keys">Keys</option>
                            <option value="Other">Other</option>
                        </select>
                    </div>
                    <div class="col-md-3">
                        <select class="form-select" id="locationFilter" onchange="app.filterItems()">
                            <option value="">All Locations</option>
                            <option value="Library">Library</option>
                            <option value="Canteen">Canteen</option>
                            <option value="Lab">Computer Lab</option>
                            <option value="Classroom">Classroom Block</option>
                            <option value="Sports">Sports Complex</option>
                            <option value="Admin">Admin Office</option>
                        </select>
                    </div>
                    <div class="col-md-2">
                        <select class="form-select" id="typeFilter" onchange="app.filterItems()">
                            <option value="">All Types</option>
                            <option value="lost">Lost</option>
                            <option value="found">Found</option>
                        </select>
                    </div>
                </div>
            </div>

            <!-- Items Grid -->
            <div class="row g-4" id="browseItemsContainer">
                <!-- Items injected here -->
            </div>
            
            <div id="noResults" class="text-center py-5 d-none">
                <i class="fas fa-ghost fa-3x text-muted mb-3"></i>
                <h5 class="text-muted">No items found matching your criteria.</h5>
            </div>
        </div>
    </section>

    <!-- REPORT PAGE -->
    <section id="report" class="page-section">
        <div class="container">
            <div class="row justify-content-center">
                <div class="col-lg-8">
                    <div class="form-container">
                        <h2 class="text-center mb-4 fw-bold text-primary-custom">Report an Item</h2>
                        <form id="reportForm" onsubmit="app.submitItem(event)">
                            
                            <div class="mb-4 text-center">
                                <label class="form-label d-block fw-bold">I am reporting a...</label>
                                <div class="btn-group w-100" role="group">
                                    <input type="radio" class="btn-check" name="itemType" id="typeLost" value="lost" checked>
                                    <label class="btn btn-outline-danger" for="typeLost">Lost Item</label>

                                    <input type="radio" class="btn-check" name="itemType" id="typeFound" value="found">
                                    <label class="btn btn-outline-warning" for="typeFound">Found Item</label>
                                </div>
                            </div>

                            <div class="row g-3">
                                <div class="col-md-6">
                                    <label class="form-label">Item Name *</label>
                                    <input type="text" class="form-control" id="itemName" required placeholder="e.g. Blue Dell Laptop">
                                </div>
                                <div class="col-md-6">
                                    <label class="form-label">Category *</label>
                                    <select class="form-select" id="itemCategory" required>
                                        <option value="" disabled selected>Select Category</option>
                                        <option value="Electronics">Electronics</option>
                                        <option value="Books">Books</option>
                                        <option value="ID Cards">ID Cards</option>
                                        <option value="Bags">Bags</option>
                                        <option value="Clothing">Clothing</option>
                                        <option value="Keys">Keys</option>
                                        <option value="Other">Other</option>
                                    </select>
                                </div>
                                
                                <div class="col-md-6">
                                    <label class="form-label">Location *</label>
                                    <select class="form-select" id="itemLocation" required>
                                        <option value="" disabled selected>Where was it lost/found?</option>
                                        <option value="Library">Library</option>
                                        <option value="Canteen">Canteen</option>
                                        <option value="Lab">Computer Lab</option>
                                        <option value="Classroom">Classroom Block</option>
                                        <option value="Sports">Sports Complex</option>
                                        <option value="Admin">Admin Office</option>
                                        <option value="Other">Other</option>
                                    </select>
                                </div>
                                <div class="col-md-6">
                                    <label class="form-label">Date *</label>
                                    <input type="date" class="form-control" id="itemDate" required>
                                </div>

                                <div class="col-12">
                                    <label class="form-label">Description</label>
                                    <textarea class="form-control" id="itemDescription" rows="3" placeholder="Provide details like color, brand, distinct marks..."></textarea>
                                </div>

                                <div class="col-12">
                                    <label class="form-label">Upload Image (Optional)</label>
                                    <input type="file" class="form-control" id="itemImageInput" accept="image/*">
                                    <div class="form-text">Images are stored locally in browser memory for this demo.</div>
                                </div>

                                <div class="col-md-6">
                                    <label class="form-label">Your Name *</label>
                                    <input type="text" class="form-control" id="reporterName" required>
                                </div>
                                <div class="col-md-6">
                                    <label class="form-label">Contact Number/Email *</label>
                                    <input type="text" class="form-control" id="reporterContact" required placeholder="Phone or Student Email">
                                </div>
                            </div>

                            <div class="d-grid gap-2 mt-4">
                                <button type="submit" class="btn btn-primary btn-lg bg-gradient-custom border-0">Submit Report</button>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- ADMIN DASHBOARD -->
    <section id="admin" class="page-section">
        <div class="container">
            <h2 class="mb-4 fw-bold text-primary-custom">Admin Dashboard</h2>
            <div class="card border-0 shadow-sm p-3">
                <div class="table-responsive">
                    <table class="table table-hover align-middle">
                        <thead class="table-light">
                            <tr>
                                <th>Status</th>
                                <th>Item</th>
                                <th>Category</th>
                                <th>Location</th>
                                <th>Date</th>
                                <th>Reporter</th>
                                <th>Actions</th>
                            </tr>
                        </thead>
                        <tbody id="adminTableBody">
                            <!-- Populated by JS -->
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </section>

    <!-- CONTACT PAGE -->
    <section id="contact" class="page-section">
        <div class="container">
            <div class="row justify-content-center">
                <div class="col-md-8 text-center">
                    <h2 class="fw-bold mb-4 text-primary-custom">Contact Support</h2>
                    <p class="lead text-muted mb-5">Have a question or need to report a bug? Reach out to the campus administration.</p>
                </div>
            </div>
            <div class="row g-5">
                <div class="col-md-5">
                    <div class="card border-0 shadow-sm h-100 p-4">
                        <h4 class="mb-4">Get in Touch</h4>
                        <div class="d-flex align-items-center mb-3">
                            <div class="bg-light p-3 rounded-circle me-3 text-primary-custom"><i class="fas fa-map-marker-alt"></i></div>
                            <div>
                                <h6 class="mb-0">Main Campus Office</h6>
                                <small class="text-muted">Building A, Room 101</small>
                            </div>
                        </div>
                        <div class="d-flex align-items-center mb-3">
                            <div class="bg-light p-3 rounded-circle me-3 text-primary-custom"><i class="fas fa-phone"></i></div>
                            <div>
                                <h6 class="mb-0">Helpline</h6>
                                <small class="text-muted">+1 (555) 123-4567</small>
                            </div>
                        </div>
                        <div class="d-flex align-items-center">
                            <div class="bg-light p-3 rounded-circle me-3 text-primary-custom"><i class="fas fa-envelope"></i></div>
                            <div>
                                <h6 class="mb-0">Email</h6>
                                <small class="text-muted">support@campusfinder.edu</small>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="col-md-7">
                    <div class="form-container h-100">
                        <form onsubmit="event.preventDefault(); app.showToast('Message sent! We will reply shortly.');">
                            <div class="mb-3">
                                <label class="form-label">Name</label>
                                <input type="text" class="form-control" required>
                            </div>
                            <div class="mb-3">
                                <label class="form-label">Email</label>
                                <input type="email" class="form-control" required>
                            </div>
                            <div class="mb-3">
                                <label class="form-label">Message</label>
                                <textarea class="form-control" rows="4" required></textarea>
                            </div>
                            <button class="btn btn-primary bg-gradient-custom border-0 w-100">Send Message</button>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer>
        <div class="container text-center">
            <div class="mb-3 social-icons">
                <a href="#"><i class="fab fa-facebook"></i></a>
                <a href="#"><i class="fab fa-twitter"></i></a>
                <a href="#"><i class="fab fa-instagram"></i></a>
            </div>
            <p class="mb-0">&copy; 2026 Campus Finder. All Rights Reserved.</p>
            <small class="text-white-50">Designed for University Student Utility</small>
        </div>
    </footer>

    <!-- Item Details Modal -->
    <div class="modal fade" id="itemModal" tabindex="-1" aria-hidden="true">
        <div class="modal-dialog modal-dialog-centered">
            <div class="modal-content">
                <div class="modal-header border-0">
                    <h5 class="modal-title fw-bold" id="modalTitle">Item Details</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    <img id="modalImage" src="" class="img-fluid rounded mb-3 w-100" style="max-height: 250px; object-fit: cover; display: none;">
                    <span id="modalBadge" class="badge mb-2"></span>
                    <h4 id="modalItemName" class="fw-bold mb-2"></h4>
                    <p class="text-muted mb-3"><i class="fas fa-map-marker-alt me-2"></i><span id="modalLocation"></span> &bull; <span id="modalDate"></span></p>
                    <p id="modalDesc" class="mb-4"></p>
                    
                    <div class="bg-light p-3 rounded">
                        <h6 class="fw-bold mb-2">Contact Reporter</h6>
                        <p class="mb-1"><strong>Name:</strong> <span id="modalReporter"></span></p>
                        <p class="mb-0"><strong>Contact:</strong> <span id="modalContact"></span></p>
                    </div>
                </div>
                <div class="modal-footer border-0">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
                    <a id="modalCallBtn" href="#" class="btn btn-primary"><i class="fas fa-phone me-2"></i>Call Now</a>
                </div>
            </div>
        </div>
    </div>

    <!-- Bootstrap Bundle JS -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>

    <script>
        /**
         * Campus Lost & Found - Application Logic
         * Uses LocalStorage for persistence.
         */
        const app = {
            data: [],
            
            // Initialize the app
            init: function() {
                this.loadData();
                this.renderItems();
                this.renderAdmin();
                this.updateStats();
                
                // Event listener for image upload preview (optional enhancement logic could go here)
            },

            // Load data from LocalStorage or set defaults
            loadData: function() {
                const storedData = localStorage.getItem('campusLostFoundData');
                if (storedData) {
                    this.data = JSON.parse(storedData);
                } else {
                    // Seed with dummy data for demonstration
                    this.data = [
                        {
                            id: 1715423001,
                            type: 'lost',
                            name: 'MacBook Air M1',
                            category: 'Electronics',
                            location: 'Library',
                            date: '2026-03-10',
                            description: 'Silver MacBook Air with a "NASA" sticker on the lid. Left it on the 2nd floor table.',
                            image: 'https://images.unsplash.com/photo-1517336714731-489689fd1ca4?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60',
                            reporter: 'Alex Johnson',
                            contact: 'alex.j@uni.edu'
                        },
                        {
                            id: 1715423002,
                            type: 'found',
                            name: 'Black Leather Wallet',
                            category: 'Bags',
                            location: 'Canteen',
                            date: '2026-03-11',
                            description: 'Found a black leather wallet near the vending machine. Contains some cash and a gym card.',
                            image: null,
                            reporter: 'Sarah Smith',
                            contact: '555-0192'
                        },
                        {
                            id: 1715423003,
                            type: 'lost',
                            name: 'Calculus Textbook',
                            category: 'Books',
                            location: 'Classroom',
                            date: '2026-03-12',
                            description: 'Calculus: Early Transcendentals, 8th Edition. Hardcover.',
                            image: null,
                            reporter: 'Mike Ross',
                            contact: 'mike.r@uni.edu'
                        }
                    ];
                    this.saveData();
                }
            },

            // Save current state to LocalStorage
            saveData: function() {
                localStorage.setItem('campusLostFoundData', JSON.stringify(this.data));
                this.updateStats();
            },

            // Navigation Logic
            showPage: function(pageId) {
                // Hide all sections
                document.querySelectorAll('.page-section').forEach(el => el.classList.remove('active'));
                document.querySelectorAll('.nav-link').forEach(el => el.classList.remove('active'));
                
                // Show target section
                document.getElementById(pageId).classList.add('active');
                
                // Highlight navbar item
                const navLink = document.querySelector(`.nav-link[href="#" onclick="app.showPage('${pageId}')"]`); // simplified selector logic
                // Actually easier to just find the link containing the text or specific ID, but let's loop
                document.querySelectorAll('.nav-link').forEach(link => {
                    if(link.getAttribute('onclick').includes(pageId)) {
                        link.classList.add('active');
                    }
                });

                if (pageId === 'home') {
                    this.renderItems(); // Refresh recent items
                } else if (pageId === 'browse') {
                    this.filterItems(); // Ensure browse is fresh
                } else if (pageId === 'admin') {
                    this.renderAdmin();
                }
                
                window.scrollTo(0,0);
            },

            // Helper to pre-select radio button on report page from Home
            prefillReport: function(type) {
                this.showPage('report');
                if(type === 'lost') {
                    document.getElementById('typeLost').checked = true;
                } else {
                    document.getElementById('typeFound').checked = true;
                }
            },

            // Add new item
            submitItem: function(event) {
                event.preventDefault();
                
                const type = document.querySelector('input[name="itemType"]:checked').value;
                const fileInput = document.getElementById('itemImageInput');
                
                // Create item object
                const newItem = {
                    id: Date.now(),
                    type: type,
                    name: document.getElementById('itemName').value,
                    category: document.getElementById('itemCategory').value,
                    location: document.getElementById('itemLocation').value,
                    date: document.getElementById('itemDate').value,
                    description: document.getElementById('itemDescription').value,
                    reporter: document.getElementById('reporterName').value,
                    contact: document.getElementById('reporterContact').value,
                    image: null 
                };

                // Handle Image File -> Base64
                if (fileInput.files && fileInput.files[0]) {
                    const reader = new FileReader();
                    reader.onload = function(e) {
                        // In a real app, you'd upload to cloud storage. 
                        // Here we resize/compress would be ideal, but for simplicity we store raw base64.
                        // Warning: LocalStorage is limited (5MB). Large images will crash it.
                        newItem.image = e.target.result; 
                        app.finalizeSubmission(newItem);
                    };
                    reader.readAsDataURL(fileInput.files[0]);
                } else {
                    // Assign a random placeholder if no image
                    newItem.image = null; 
                    this.finalizeSubmission(newItem);
                }
            },

            finalizeSubmission: function(item) {
                this.data.unshift(item); // Add to beginning
                this.saveData();
                document.getElementById('reportForm').reset();
                this.showToast(`${item.type === 'lost' ? 'Lost' : 'Found'} item reported successfully!`);
                this.showPage('browse');
            },

            // Render Items for Home (Recent) and Browse (All/Filtered)
            renderItems: function(itemsToRender = this.data) {
                const recentContainer = document.getElementById('recentItemsContainer');
                const browseContainer = document.getElementById('browseItemsContainer');
                
                // Clear containers
                if(recentContainer) recentContainer.innerHTML = '';
                if(browseContainer) browseContainer.innerHTML = '';

                // Render logic
                const createCard = (item) => {
                    const badgeClass = item.type === 'lost' ? 'badge-lost' : 'badge-found';
                    const badgeText = item.type === 'lost' ? 'LOST' : 'FOUND';
                    const fallbackImg = item.type === 'lost' 
                        ? 'https://via.placeholder.com/500x300/e63946/ffffff?text=No+Image' 
                        : 'https://via.placeholder.com/500x300/f7c948/0d2c54?text=No+Image';
                    
                    const imgUrl = item.image ? item.image : fallbackImg;

                    return `
                        <div class="col-md-6 col-lg-4">
                            <div class="card item-card h-100">
                                <div class="position-relative">
                                    <img src="${imgUrl}" class="card-img-top" alt="${item.name}">
                                    <span class="badge ${badgeClass} position-absolute top-0 end-0 m-3 px-3 py-2 rounded-pill">${badgeText}</span>
                                </div>
                                <div class="card-body">
                                    <div class="d-flex justify-content-between align-items-start mb-2">
                                        <small class="text-muted"><i class="far fa-calendar-alt me-1"></i> ${item.date}</small>
                                        <small class="text-primary fw-bold"><i class="fas fa-tag me-1"></i> ${item.category}</small>
                                    </div>
                                    <h5 class="card-title fw-bold text-dark">${item.name}</h5>
                                    <p class="card-text text-muted small"><i class="fas fa-map-marker-alt me-1"></i> ${item.location}</p>
                                    <p class="card-text text-truncate">${item.description}</p>
                                </div>
                                <div class="card-footer border-0 bg-white pb-3 pt-0">
                                    <button class="btn btn-outline-primary w-100 rounded-pill" onclick="app.viewDetails(${item.id})">
                                        View Details
                                    </button>
                                </div>
                            </div>
                        </div>
                    `;
                };

                // Home Page: Show top 3 recent
                if(recentContainer && document.getElementById('home').classList.contains('active')) {
                   this.data.slice(0, 3).forEach(item => {
                       recentContainer.innerHTML += createCard(item);
                   });
                   if(this.data.length === 0) recentContainer.innerHTML = '<p class="text-center text-muted">No items reported yet.</p>';
                }

                // Browse Page: Show filtered
                if(browseContainer) {
                    if (itemsToRender.length === 0) {
                        document.getElementById('noResults').classList.remove('d-none');
                    } else {
                        document.getElementById('noResults').classList.add('d-none');
                        itemsToRender.forEach(item => {
                            browseContainer.innerHTML += createCard(item);
                        });
                    }
                }
            },

            // Filter logic
            filterItems: function() {
                const search = document.getElementById('searchInput').value.toLowerCase();
                const cat = document.getElementById('categoryFilter').value;
                const loc = document.getElementById('locationFilter').value;
                const type = document.getElementById('typeFilter').value;

                const filtered = this.data.filter(item => {
                    const matchesSearch = item.name.toLowerCase().includes(search) || item.description.toLowerCase().includes(search);
                    const matchesCat = cat === "" || item.category === cat;
                    const matchesLoc = loc === "" || item.location === loc;
                    const matchesType = type === "" || item.type === type;
                    return matchesSearch && matchesCat && matchesLoc && matchesType;
                });

                this.renderItems(filtered);
            },

            // Admin Table Render
            renderAdmin: function() {
                const tbody = document.getElementById('adminTableBody');
                tbody.innerHTML = '';
                
                this.data.forEach(item => {
                    const badgeClass = item.type === 'lost' ? 'bg-danger' : 'bg-warning text-dark';
                    const row = `
                        <tr>
                            <td><span class="badge ${badgeClass}">${item.type.toUpperCase()}</span></td>
                            <td class="fw-bold">${item.name}</td>
                            <td>${item.category}</td>
                            <td>${item.location}</td>
                            <td>${item.date}</td>
                            <td>${item.reporter}<br><small class="text-muted">${item.contact}</small></td>
                            <td>
                                <button class="btn btn-sm btn-outline-danger" onclick="app.deleteItem(${item.id})">
                                    <i class="fas fa-trash"></i>
                                </button>
                            </td>
                        </tr>
                    `;
                    tbody.innerHTML += row;
                });
            },

            // View Item Details Modal
            viewDetails: function(id) {
                const item = this.data.find(i => i.id === id);
                if(!item) return;

                document.getElementById('modalTitle').innerText = item.type === 'lost' ? 'Lost Item Details' : 'Found Item Details';
                document.getElementById('modalItemName').innerText = item.name;
                document.getElementById('modalLocation').innerText = item.location;
                document.getElementById('modalDate').innerText = item.date;
                document.getElementById('modalDesc').innerText = item.description;
                document.getElementById('modalReporter').innerText = item.reporter;
                document.getElementById('modalContact').innerText = item.contact;
                
                const imgEl = document.getElementById('modalImage');
                if(item.image) {
                    imgEl.src = item.image;
                    imgEl.style.display = 'block';
                } else {
                    imgEl.style.display = 'none';
                }

                // Badge
                const badge = document.getElementById('modalBadge');
                badge.className = `badge mb-2 ${item.type === 'lost' ? 'bg-danger' : 'bg-warning text-dark'}`;
                badge.innerText = item.type.toUpperCase();

                // Call Button
                const callBtn = document.getElementById('modalCallBtn');
                callBtn.href = `tel:${item.contact}`; // Simple tel link

                const modal = new bootstrap.Modal(document.getElementById('itemModal'));
                modal.show();
            },

            // Delete Item
            deleteItem: function(id) {
                if(confirm('Are you sure you want to delete this report?')) {
                    this.data = this.data.filter(i => i.id !== id);
                    this.saveData();
                    this.renderAdmin();
                    this.showToast('Item removed successfully.');
                }
            },

            // Update Stats counters
            updateStats: function() {
                const total = this.data.length;
                const lost = this.data.filter(i => i.type === 'lost').length;
                const found = this.data.filter(i => i.type === 'found').length;

                document.getElementById('totalItemsCount').innerText = total;
                document.getElementById('lostItemsCount').innerText = lost;
                document.getElementById('foundItemsCount').innerText = found;
            },

            // Utility: Show Toast
            showToast: function(msg) {
                document.getElementById('toastMessage').innerText = msg;
                const toast = new bootstrap.Toast(document.getElementById('liveToast'));
                toast.show();
            }
        };

        // Initialize App on Load
        document.addEventListener('DOMContentLoaded', () => {
            app.init();
        });

    </script>
</body>
</html>

