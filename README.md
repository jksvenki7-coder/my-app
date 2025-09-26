# my-app
freshtohome
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Freshfoods Dashboard</title>
    <style>
        body { font-family: Arial, sans-serif; margin:0; background:#f5f6fa; }
        #container { display: flex; min-height:100vh;}
        #sidebar {
            width: 200px; background: #292b2c; color: #fff; padding: 30px 10px; min-height:100vh;
            display:flex; flex-direction:column; gap: 20px;
        }
        #sidebar button {
            background: #444; color: #fff; border: none; padding: 10px 15px; font-size: 16px;
            border-radius: 5px; cursor: pointer; transition:background 0.3s;
        }
        #sidebar button:hover { background: #007bff;}
        #main-content { flex:1; padding: 40px;}
        .hidden { display:none;}
        input, textarea { width: 300px; padding:8px; margin:10px 0;}
        label { display:block; margin-top:12px;}
        #order-list { background:#fff; padding:10px; border-radius:10px; margin-top:20px;}
    </style>
</head>
<body>
<div id="container">
    <div id="sidebar">
        <button onclick="showSection('home')">Home</button>
        <button onclick="showSection('groceries')">Groceries</button>
        <button onclick="showSection('camera')">Camera</button>
        <button onclick="showSection('orders')">Orders</button>
        <button onclick="showSection('contact')">Contact</button>
        <button style="margin-top:auto;" onclick="showSection('profile')">Profile</button>
    </div>function submitOrder() {
    const name = document.getElementById('name').value.trim();
    const mobile = document.getElementById('mobile').value.trim();
    const order = document.getElementById('order').value.trim();
    const address = document.getElementById('address').value.trim();

    if (!name) {
        alert('Please enter your name.');
        return;
    }
    if (!mobile || !/^\d{10}$/.test(mobile)) {
        alert('Please enter a valid 10-digit mobile number.');
        return;
    }
    if (!order) {
        alert('Please enter your order details.');
        return;
    }
    if (!address) {
        alert('Please enter your delivery address.');
        return;
    }

    document.getElementById('order-list').innerHTML = `
        <strong>Order Details:</strong><br>
        Name: ${name}<br>
        Mobile: ${mobile}<br>
        Order: ${order}<br>
        Address: ${address}
    `;

    showSection('orders');
}
    <div id="main-content">
        <!-- Home Section -->
        <div id="home-section">
            <h2>Welcome to Freshfoods!</h2>
            <p>All items view and info.</p>
        </div>
        <!-- Groceries Section -->
        <div id="groceries-section" class="hidden">
            <h2>Groceries</h2>
            <ul>
                <li>Rice</li>
                <li>Pulses</li>
                <li>Wheat Flour</li>
                <li>Spices</li>
                <!-- Add more -->
            </ul>
        </div>
        <!-- Camera Section -->
        <div id="camera-section" class="hidden">
            <h2>Open Camera</h2>
            <video id="video" width="320" height="240" autoplay></video>
            <button onclick="capturePhoto()">Capture</button>
            <canvas id="canvas" width="320" height="240" style="display:none;"></canvas>
            <img id="photo" src="" alt="Photo" style="display:block;margin-top:10px;max-width:320px;">
            <script>
                // Camera open logic
                const video = document.getElementById('video');
                if (navigator.mediaDevices && navigator.mediaDevices.getUserMedia) {
                    navigator.mediaDevices.getUserMedia({ video: true }).then(function(stream) {
                        video.srcObject = stream;
                        video.play();
                    });
                }
                function capturePhoto() {
                    var canvas = document.getElementById('canvas');
                    var context = canvas.getContext('2d');
                    context.drawImage(video, 0, 0, 320, 240);
                    // Show the captured photo
                    document.getElementById('photo').src = canvas.toDataURL('image/png');
                }
            </script>
        </div>
        <!-- Orders Section -->
        <div id="orders-section" class="hidden">
            <h2>Your Orders</h2>
            <div id="order-list">No orders yet.</div>
        </div>
        <!-- Contact Section -->
        <div id="contact-section" class="hidden">
            <h2>Contact Us</h2>
            <p>Call us: 8917143043</p>
            <p>Email: support@freshfoods.com</p>
        </div>
        <!-- Profile Section -->
        <div id="profile-section" class="hidden">
            <h2>Profile</h2>
            <form id="order-form">
                <label>Name:</label>
                <input type="text" id="name" required>
                <label>Mobile Number:</label>
                <input type="text" id="mobile" required>
                <label>Order:</label>
                <input type="text" id="order">
                <label>Delivery Address:</label>
                <textarea id="address"></textarea>
                <button type="button" onclick="submitOrder()">Submit Order</button>
            </form>
        </div>
    </div>
</div>
<script>
    function showSection(section) {
        const sections = ['home','groceries','camera','orders','contact','profile'];
        sections.forEach(s=>{
            document.getElementById(s+'-section').classList.add('hidden');
        });
        document.getElementById(section+'-section').classList.remove('hidden');
    }

    // Order form logic
    function submitOrder() {
        const name = document.getElementById('name').value;
        const mobile = document.getElementById('mobile').value;
        const order = document.getElementById('order').value;
        const address = document.getElementById('address').value;
        document.getElementById('order-list').innerHTML = `
            <strong>Order Details:</strong><br>
            Name: ${name}<br>
            Mobile: ${mobile}<br>
            Order: ${order}<br>
            Address: ${address}
        `;
        // Switch to Orders tab
        showSection('orders');
    }
</script>
</body>
</html>
