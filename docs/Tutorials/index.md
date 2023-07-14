<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Grid Posts with Sliders</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/slick-carousel/1.9.0/slick.min.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/slick-carousel/1.9.0/slick-theme.min.css">
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f5f5f5;
        }

        .grid-container {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            grid-gap: 20px;
            margin: 20px;
        }

        .post {
            background-color: #fff;
            border-radius: 5px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            padding: 20px;
            transition: transform 0.3s ease-in-out;
            text-align: center;
        }

        .post:hover {
            transform: translateY(-5px);
        }

        .post img {
            max-width: 100%;
            border-radius: 5px;
            margin-bottom: 10px;
        }

        .post h3 {
            font-size: 18px;
            margin-bottom: 10px;
            color: #333;
        }

        .post p {
            font-size: 14px;
            color: #666;
            margin-bottom: 15px;
        }

        .slick-dots {
            bottom: -25px;
        }

        .slick-dots li button:before {
            font-size: 10px;
            color: #999;
        }

        .slick-dots li.slick-active button:before {
            color: #555;
        }
    </style>
</head>
<body>
    <div class="grid-container">
        <div class="post">
            <img src="https://via.placeholder.com/300" alt="Post 1">
            <h3>Post 1</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
        </div>
        <div class="post">
            <img src="https://via.placeholder.com/300" alt="Post 2">
            <h3>Post 2</h3>
            <p>Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
        </div>
        <div class="post">
            <img src="https://via.placeholder.com/300" alt="Post 3">
            <h3>Post 3</h3>
            <p>Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris.</p>
        </div>
        <!-- Add more posts as needed -->
    </div>

    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/slick-carousel/1.9.0/slick.min.js"></script>
    <script>
        $(document).ready(function(){
            $('.grid-container').slick({
                dots: true,
                infinite: true,
                speed: 500,
                slidesToShow: 3,
                slidesToScroll: 3,
                responsive: [
                    {
                        breakpoint: 768,
                        settings: {
                            slidesToShow: 2,
                            slidesToScroll: 2
                        }
                    },
                    {
                        breakpoint: 480,
                        settings: {
                            slidesToShow: 1,
                            slidesToScroll: 1
                        }
                    }
                ]
            });
        });
    </script>
</body>
</html>
