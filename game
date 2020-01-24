const cvs = document.getElementById("campo");
  const ctx = cvs.getContext("2d");

  const box = 20;
  let snake = [];
  let keyA;
  let score = 0;
  let level = 150;

  let life = 0;
  let timeLife = 50;
  let lifeRandom = Math.floor(Math.random()*40);


  snake[0] = {
    x:15*box ,
    y:15*box
  };

  let food = {
    x: Math.floor(Math.random()*30)*box,
    y: Math.floor(Math.random()*30)*box
  };

  let lifeLocation = {
    x: Math.floor(Math.random()*30)*box,
    y: Math.floor(Math.random()*30)*box
  };

  let snakeX = snake[0].x;
  let snakeY = snake[0].y;

  window.addEventListener("keydown", function(e){
    let keyC = e.keyCode;
    if(keyC == 37 && keyA != "RIGHT") keyA = "LEFT";
    if(keyC == 38 && keyA != "DOWN") keyA = "UP";
    if(keyC == 39 && keyA != "LEFT") keyA = "RIGHT";
    if(keyC == 40 && keyA != "UP") keyA = "DOWN";
  });

  function colision(head,arraY){
    for(let i=0;i<arraY.length;i++){
      if(head.x == arraY[i].x && head.y == arraY[i].y){
        return true;
      }
    }
    return false;
  }

  function play(){
    ctx.fillStyle = "#979980";
    ctx.fillRect(0,0,600,600);

    if(keyA == "LEFT") snakeX -= box;
    if(keyA == "UP") snakeY -= box;
    if(keyA == "RIGHT") snakeX += box;
    if(keyA == "DOWN") snakeY += box;

    for(let i=0; i<snake.length; i++){
      ctx.strokeStyle = "#000";
      ctx.strokeRect(snake[i].x,snake[i].y, box, box);
      ctx.fillStyle = "#111";
      ctx.fillRect(snake[i].x+3,snake[i].y+3, 14, 14);
    }

    ctx.strokeStyle = "#000";
    ctx.strokeRect(food.x,food.y, box, box);			
    ctx.fillStyle = "#444";
    ctx.fillRect(food.x+3,food.y+3, 14, 14);

    let head = {
      x: snakeX,
      y: snakeY
    }

    if(snakeX == food.x && snakeY == food.y){
      food = {
        x: Math.floor(Math.random()*30)*box,
        y: Math.floor(Math.random()*30)*box
      };
      score++;
      level -= 5;
      clearInterval(now);
      now = setInterval(play, level);
    }else{
      snake.pop();
    }

    if(lifeRandom == 5){
      ctx.strokeStyle = "red";
      ctx.strokeRect(lifeLocation.x,lifeLocation.y, box, box);
      ctx.fillStyle = "red";
      ctx.fillRect(lifeLocation.x+3,lifeLocation.y+3, 14, 14);
      timeLife--;
      if(timeLife < 0){
        ctx.clearRect(lifeLocation.x,lifeLocation.y, box, box);
        lifeLocation = {
          x: Math.floor(Math.random()*30)*box,
          y: Math.floor(Math.random()*30)*box
        };
        lifeRandom = Math.floor(Math.random()*100);
        timeLife = 50;
      }
      if(snakeX == lifeLocation.x && snakeY == lifeLocation.y){
        life++;
        ctx.clearRect(lifeLocation.x,lifeLocation.y, box, box);
        lifeLocation = {
          x: Math.floor(Math.random()*30)*box,
          y: Math.floor(Math.random()*30)*box
        };
        lifeRandom = Math.floor(Math.random()*100);
        timeLife = 50;
      }
    }else{
      lifeRandom = Math.floor(Math.random()*100);
    }

    if(snakeX < 0 || snakeY < 0 || snakeX >= 600 || snakeY >= 600 || colision(head,snake)){
      if(life <= 0){
        clearInterval(now);
        document.getElementById("score").innerText = score;
        document.getElementById("telaFinal").style.display = "block";
      }else{
        if(keyA == "LEFT" && snakeY >= box && snakeY <= 600){
          snakeY -= box;
          keyA = "RIGHT";
        }else if(keyA == "LEFT" && snakeY <= (600-box)){
          snakeY += box;
          keyA = "RIGHT";
        }else if(keyA == "DOWN" && snakeX >= box && snakeX <= 600){
          snakeX -= box;
          keyA = "UP";
        }else if(keyA == "DOWN" && snakeX <= (600-box)){
          snakeX += box;
          keyA = "UP";
        }else if(keyA == "RIGHT" && snakeY >= box && snakeY <= 600){
          snakeY -= box;
          keyA = "LEFT";
        }else if(keyA == "RIGHT" && snakeY <= (600-box)){
          snakeY += box;
          keyA = "LEFT";
        }else if(keyA == "UP" && snakeX >= box && snakeX <= 600){
          snakeX -= box;
          keyA = "DOWN";
        }else if(keyA == "UP" && snakeX <= (600-box)){
          snakeX += box;
          keyA = "DOWN";
        }
        life--;
      }
    }

    ctx.fillStyle = "black";
    ctx.font = "15px Arial";
    ctx.fillText("Pontos: "+score,10,20);
    ctx.fillText("Vidas: "+life,100,20);

    snake.unshift(head);
  }

  let now = setInterval(play, level);
