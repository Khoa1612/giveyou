<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dành cho Em Yêu</title>
    <style>
        /* CSS bắt đầu từ đây */
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            background: linear-gradient(to right, #ffafbd, #ffc3a0); /* Gradient màu hồng cam */
            color: #333;
            overflow: hidden; /* Ngăn cuộn */
        }

        .screen {
            display: none;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            width: 90%;
            max-width: 400px;
            padding: 30px;
            border-radius: 15px;
            background-color: rgba(255, 255, 255, 0.95);
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
            text-align: center;
            animation: fadeIn 0.5s ease-out;
        }

        .screen.active {
            display: flex;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Màn hình chào */
        #welcome-screen h1 {
            color: #e91e63; /* Màu hồng */
            margin-bottom: 30px;
            font-size: 2.5em;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.1);
        }

        #start-button {
            background-color: #e91e63;
            color: white;
            border: none;
            padding: 15px 30px;
            font-size: 1.1em;
            border-radius: 25px;
            cursor: pointer;
            transition: background-color 0.3s ease, transform 0.2s ease;
        }

        #start-button:hover {
            background-color: #d81b60;
            transform: translateY(-3px);
        }

        /* Màn hình nhập mật khẩu */
        #passcode-screen h2 {
            color: #673ab7; /* Màu tím */
            margin-bottom: 30px;
            font-size: 1.8em;
        }

        .passcode-display {
            display: flex;
            margin-bottom: 40px;
            gap: 15px;
        }

        .passcode-display .dot {
            width: 25px;
            height: 25px;
            border-radius: 50%;
            border: 2px solid #9c27b0; /* Màu tím */
            background-color: transparent;
            transition: background-color 0.2s ease;
        }

        .passcode-display .dot.filled {
            background-color: #9c27b0;
        }

        .keypad {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 15px;
            width: 100%;
        }

        .key {
            background-color: #f3e5f5; /* Màu tím nhạt */
            color: #6a1b9a; /* Màu tím đậm */
            border: none;
            padding: 25px 0;
            font-size: 1.5em;
            border-radius: 10px;
            cursor: pointer;
            transition: background-color 0.2s ease, transform 0.1s ease;
            box-shadow: 0 3px 5px rgba(0, 0, 0, 0.1);
        }

        .key:active {
            background-color: #e1bee7;
            transform: scale(0.98);
        }

        .key.empty {
            background-color: transparent;
            cursor: default;
            box-shadow: none;
        }

        .key.delete {
            background-color: #ffccbc; /* Màu cam nhạt */
            color: #d84315; /* Màu cam đậm */
        }

        .key.delete:active {
            background-color: #ffab91;
        }

        .error-message {
            color: #f44336; /* Màu đỏ */
            margin-top: 20px;
            font-weight: bold;
            opacity: 0;
            transition: opacity 0.3s ease;
        }

        .error-message.show {
            opacity: 1;
        }

        /* Màn hình chính */
        #main-screen h1 {
            color: #4caf50; /* Màu xanh lá cây */
            margin-bottom: 20px;
            font-size: 2.2em;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.1);
        }

        .info-card {
            background-color: #e8f5e9; /* Màu xanh lá cây nhạt */
            border-left: 5px solid #4caf50;
            padding: 15px 20px;
            margin-bottom: 15px;
            border-radius: 8px;
            width: 100%;
            text-align: left;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.08);
        }

        .info-card h3 {
            color: #388e3c; /* Màu xanh lá cây đậm */
            margin-top: 0;
            margin-bottom: 5px;
            font-size: 1.1em;
        }

        .info-card p {
            margin: 0;
            line-height: 1.5;
            color: #555;
        }

        #random-message {
            background-color: #fff9c4; /* Màu vàng nhạt */
            border-left: 5px solid #ffeb3b;
            padding: 15px;
            margin-top: 20px;
            margin-bottom: 20px;
            border-radius: 8px;
            font-style: italic;
            color: #795548; /* Màu nâu */
            font-size: 1.1em;
        }

        .image-carousel {
            width: 100%;
            height: 200px; /* Chiều cao cố định cho carousel */
            overflow: hidden;
            border-radius: 10px;
            margin-bottom: 20px;
            position: relative;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }

        .carousel-image {
            width: 100%;
            height: 100%;
            object-fit: cover; /* Giúp ảnh không bị méo */
            display: none;
            opacity: 0;
            transition: opacity 1s ease-in-out;
            position: absolute;
            top: 0;
            left: 0;
        }

        .carousel-image.active {
            display: block;
            opacity: 1;
        }

        #hug-button {
            background-color: #ff5722; /* Màu cam đậm */
            color: white;
            border: none;
            padding: 12px 25px;
            font-size: 1em;
            border-radius: 20px;
            cursor: pointer;
            margin-top: 15px;
            margin-bottom: 15px; /* Thêm khoảng cách */
            transition: background-color 0.3s ease, transform 0.2s ease;
        }

        #hug-button:hover {
            background-color: #e64a19;
            transform: translateY(-2px);
        }

        #logout-button {
            background-color: #f44336;
            color: white;
            border: none;
            padding: 12px 25px;
            font-size: 1em;
            border-radius: 20px;
            cursor: pointer;
            margin-top: 10px; /* Giảm khoảng cách nếu có nhiều nút */
            transition: background-color 0.3s ease, transform 0.2s ease;
        }

        #logout-button:hover {
            background-color: #d32f2f;
            transform: translateY(-2px);
        }
        /* CSS kết thúc ở đây */
    </style>
</head>
<body>
    <div id="welcome-screen" class="screen active">
        <h1>Chào Em Yêu!</h1>
        <button id="start-button">Bấm để bắt đầu</button>
    </div>

    <div id="passcode-screen" class="screen">
        <h2>Nhập mật khẩu của chúng mình</h2>
        <div class="passcode-display">
            <span class="dot"></span>
            <span class="dot"></span>
            <span class="dot"></span>
            <span class="dot"></span>
        </div>
        <div class="keypad">
            <button class="key">1</button>
            <button class="key">2</button>
            <button class="key">3</button>
            <button class="key">4</button>
            <button class="key">5</button>
            <button class="key">6</button>
            <button class="key">7</button>
            <button class="key">8</button>
            <button class="key">9</button>
            <button class="key empty"></button> <button class="key">0</button>
            <button class="key delete">Xóa</button>
        </div>
        <p id="error-message" class="error-message"></p>
    </div>

    <div id="main-screen" class="screen">
        <h1>Thông tin cute về Em Yêu!</h1>

        <div class="image-carousel">
            <img src="https://via.placeholder.com/400x200/FFB6C1/FFFFFF?text=Anh+%26+Em+1" alt="Kỷ niệm 1" class="carousel-image active">
            <img src="https://via.placeholder.com/400x200/ADD8E6/FFFFFF?text=Kỷ+niệm+của+chúng+ta+2" alt="Kỷ niệm 2" class="carousel-image">
            <img src="https://via.placeholder.com/400x200/90EE90/FFFFFF?text=Những+khoảnh+khắc+đẹp+3" alt="Kỷ niệm 3" class="carousel-image">
            <img src="https://via.placeholder.com/400x200/FFD700/FFFFFF?text=Yêu+Em+rất+nhiều+4" alt="Kỷ niệm 4" class="carousel-image">
        </div>

        <div id="random-message"></div>

        <div class="info-card">
            <h3>Tên Em:</h3>
            <p>Nguyễn Thị Yêu</p>
        </div>
        <div class="info-card">
            <h3>Ngày sinh nhật:</h3>
            <p>16/12/2000</p>
        </div>
        <div class="info-card">
            <h3>Sở thích:</h3>
            <p>Thích anh, nghe nhạc, đọc sách, nấu ăn, du lịch...</p>
        </div>
        <div class="info-card">
            <h3>Điều anh yêu nhất ở em:</h3>
            <p>Nụ cười của em, sự quan tâm của em, và mọi thứ thuộc về em!</p>
        </div>

        <button id="hug-button">Nhận một cái ôm từ anh</button>
        <button id="logout-button">Đăng xuất</button>

        <audio id="background-music" loop>
            <source src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3" type="audio/mpeg">
            Trình duyệt của bạn không hỗ trợ thẻ audio.
        </audio>
    </div>

    <script>
        // JavaScript bắt đầu từ đây
        document.addEventListener('DOMContentLoaded', () => {
            const welcomeScreen = document.getElementById('welcome-screen');
            const startButton = document.getElementById('start-button');
            const passcodeScreen = document.getElementById('passcode-screen');
            const mainScreen = document.getElementById('main-screen');
            const keypad = document.querySelector('.keypad');
            const passcodeDots = document.querySelectorAll('.passcode-display .dot');
            const errorMessage = document.getElementById('error-message');
            const logoutButton = document.getElementById('logout-button');
            const backgroundMusic = document.getElementById('background-music');
            const carouselImages = document.querySelectorAll('.carousel-image');
            const randomMessageDiv = document.getElementById('random-message');
            const hugButton = document.getElementById('hug-button');


            const correctPasscode = "1612"; // Mật khẩu đúng
            let enteredPasscode = ""; // Mật khẩu người dùng nhập
            let currentImageIndex = 0;
            let carouselInterval; // Biến để lưu interval của carousel

            const romanticMessages = [
                "Em là ánh nắng của cuộc đời anh!",
                "Mỗi ngày có em là một ngày tuyệt vời.",
                "Anh yêu em nhiều hơn những gì anh có thể nói.",
                "Em là người duy nhất thấu hiểu anh.",
                "Nụ cười của em là động lực của anh.",
                "Hãy cùng nhau tạo thêm thật nhiều kỷ niệm nhé!",
                "Anh luôn ở đây vì em."
            ];

            // Hàm chuyển đổi màn hình
            function showScreen(screenId) {
                document.querySelectorAll('.screen').forEach(screen => {
                    screen.classList.remove('active');
                });
                document.getElementById(screenId).classList.add('active');

                // Xử lý nhạc và carousel khi vào màn hình chính
                if (screenId === 'main-screen') {
                    backgroundMusic.play().catch(e => console.log("Lỗi phát nhạc:", e)); // Cố gắng phát nhạc
                    startCarousel(); // Bắt đầu carousel
                    displayRandomMessage(); // Hiển thị lời nhắn ngẫu nhiên
                } else {
                    backgroundMusic.pause(); // Dừng nhạc khi rời màn hình chính
                    backgroundMusic.currentTime = 0; // Đặt lại về đầu
                    stopCarousel(); // Dừng carousel
                }
            }

            // Xử lý sự kiện khi bấm nút "Bắt đầu"
            startButton.addEventListener('click', () => {
                showScreen('passcode-screen');
            });

            // Xử lý khi bấm các phím số trên bàn phím
            keypad.addEventListener('click', (event) => {
                const target = event.target;
                if (target.classList.contains('key') && !target.classList.contains('empty')) {
                    if (target.classList.contains('delete')) {
                        // Xóa ký tự cuối cùng
                        enteredPasscode = enteredPasscode.slice(0, -1);
                    } else {
                        // Thêm số vào mật khẩu đã nhập
                        if (enteredPasscode.length < correctPasscode.length) {
                            enteredPasscode += target.textContent;
                        }
                    }
                    updatePasscodeDisplay();
                    checkPasscode();
                }
            });

            // Cập nhật hiển thị các chấm mật khẩu
            function updatePasscodeDisplay() {
                passcodeDots.forEach((dot, index) => {
                    if (index < enteredPasscode.length) {
                        dot.classList.add('filled');
                    } else {
                        dot.classList.remove('filled');
                    }
                });
                // Ẩn thông báo lỗi khi người dùng bắt đầu nhập lại
                errorMessage.classList.remove('show');
            }

            // Kiểm tra mật khẩu
            function checkPasscode() {
                if (enteredPasscode.length === correctPasscode.length) {
                    if (enteredPasscode === correctPasscode) {
                        // Mật khẩu đúng, chuyển sang màn hình chính
                        setTimeout(() => {
                            showScreen('main-screen');
                            enteredPasscode = ""; // Reset mật khẩu
                            updatePasscodeDisplay(); // Reset hiển thị chấm
                        }, 300); // Chờ một chút trước khi chuyển màn hình
                    } else {
                        // Mật khẩu sai, hiển thị lỗi và reset
                        errorMessage.textContent = "Mật khẩu sai rồi Em Yêu, thử lại nhé!";
                        errorMessage.classList.add('show');
                        enteredPasscode = ""; // Reset mật khẩu
                        setTimeout(() => {
                            updatePasscodeDisplay(); // Reset hiển thị chấm sau 1 giây
                        }, 1000);
                    }
                }
            }

            // Carousel ảnh
            function startCarousel() {
                if (carouselImages.length === 0) return;

                carouselInterval = setInterval(() => {
                    carouselImages[currentImageIndex].classList.remove('active');
                    currentImageIndex = (currentImageIndex + 1) % carouselImages.length;
                    carouselImages[currentImageIndex].classList.add('active');
                }, 3000); // Chuyển ảnh sau mỗi 3 giây
            }

            function stopCarousel() {
                clearInterval(carouselInterval);
            }

            // Hiển thị lời nhắn ngẫu nhiên
            function displayRandomMessage() {
                const randomIndex = Math.floor(Math.random() * romanticMessages.length);
                randomMessageDiv.textContent = romanticMessages[randomIndex];
            }

            // Xử lý nút "Nhận một cái ôm"
            hugButton.addEventListener('click', () => {
                alert("Bạn đã nhận được một cái ôm ấm áp từ anh! 🤗");
            });

            // Xử lý khi bấm nút "Đăng xuất"
            logoutButton.addEventListener('click', () => {
                showScreen('welcome-screen');
                enteredPasscode = ""; // Đảm bảo mật khẩu được reset
                updatePasscodeDisplay(); // Cập nhật hiển thị chấm
            });
        });
        // JavaScript kết thúc ở đây
    </script>
</body>
</html>
