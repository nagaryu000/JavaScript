# JavaScript
<!DOCTYPE html>
<html lang="ja">
  <head>
    <meta charset="utf-8">
    <title>Flash Cards!</title>
    <style media="screen">
      body {
        margin: 0;
        background: #e0e0e0;
        text-align: center;;
        font-family: Verdana, sans-serif;
        color: #fff;
      }
      #btn {
        width: 200px;
        margin: 0 auto;
        padding: 7px;
        border-radius: 5px;
        background: #00aaff;
        box-shadow: 0 4px 0 #0088cc;
        cursor: pointer;
      }
      #btn:hover {
        opacity: 0.8;
      }
      #card {
        margin: 60px auto 20px;
        width: 400px;
        height: 100px;
        cursor: pointer;
        font-size: 40px;
        line-height: 100px;
        perspective: 100px;
        transform-style: preserve-3d;
        transition: transform .8s;
      }
      #card-front, #card-back {
        display: block;
        width: 100%;
        height: 100%;
        border-radius: 5px;
        position: absolute;
        backface-visibility: hidden;
      }
      #card-front {
        background: #fff;
        color: #333;
      }
      #card-back {
        background: #00aaff;
        transform: rotateY(180deg);
      }
      .open {
        transform: rotateY(180deg);
      }
    </style>
  </head>
  <body>
    <div id="card">
      <div id="card-front">
        front
      </div>
      <div id="card-back">
        back
      </div>
    </div>
    <div id="btn">
      NEXT
    </div>
    <script>
      (function() {
        'use strict';

        var words = [
          {'en': 'read', 'ja': '読む'},
          {'en': 'write', 'ja': '書く'},
          {'en': 'eat', 'ja': '食べる'},
          {'en': 'run', 'ja': '走る'},
          {'en': 'walk', 'ja': '歩く'}
        ];

        var card = document.getElementById('card');
        var cardFront = document.getElementById('card-front');
        var cardBack = document.getElementById('card-back');
        var btn = document.getElementById('btn');
        card.addEventListener('click', function() {
          flip();
        });
        btn.addEventListener('click', function() {
          next();
        });

        function next() {
          if (card.className === 'open') {
            card.addEventListener('transitionend', setCard);
            flip();
          } else {
            setCard();
          }
        }

        function setCard() {
          var num = Math.floor(Math.random() * words.length);
          cardFront.innerHTML = words[num]['en'];
          cardBack.innerHTML = words[num]['ja'];
          card.removeEventListener('transitionend', setCard);
        }

        setCard();

        window.addEventListener('keyup', function(e) {
          // e.keycode
          // f: 70
          // n: 78
          // console.log(e.keycode)
          if (e.keyCode === 70) {
            flip();
          } else if (e.keyCode === 78){
            next();
          }
        });

        function flip() {
          card.className = card.className === '' ? 'open' : '';
        }

      })();

    </script>
  </body>
</html>
