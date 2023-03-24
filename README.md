//ponginjvs
//Game Pong in JavaScript, project created through Alura's course, using the JavaScript language. 
//Creator: Clodoaldo Junior

//variáveis da bolinha
let xBolinha = 300;
let yBolinha = 200;
let diametro = 13;
let raio = diametro / 2;

//variáveis da velocidade da bolinha
let velocidadeXBolinha = 6;
let velocidadeYBolinha= 6;

//variáveis da raquete
let xRaquete = 0;
let yRaquete = 150;
let raqueteComprimento = 10;
let raqueteAltura = 75;

//variáveis do oponente
let xRaqueteOponente = 583;
let yRaqueteOponente = 150;
let velocidadeYOponente;

let colidiu = false;

//placar do jogo
let meusPontos = 0;
let pontosOponentes = 0;

//sons do jogos
let raquetada;
let ponto;
let trilha;

function preload (){
  trilha = loadSound ("Trilha Sonora.wav");
  ponto = loadSound ("ponto.mp3");
  raquetada = loadSound ("raquetada.mp3");
}

function setup() {
  createCanvas(600, 400);
  trilha.loop();
}

function draw() {
  background(0);
  
  mostraBolinha();
  movimentaBolinha();
  verificaColisaoBorda();
  
  mostraRaquete(xRaquete, yRaquete);
  mostraRaquete(xRaqueteOponente, yRaqueteOponente);
  
  movimentaMinhaRaquete();
  movimentaRaqueteOponente();
  
  verificaColisaoRaquete(xRaquete, yRaquete);
  verificaColisaoRaquete(xRaqueteOponente, yRaqueteOponente);
  
  incluiPlacar();
  marcaPonto();

}

  function mostraBolinha(){
    circle(xBolinha,yBolinha,diametro);
  }

  function movimentaBolinha(){
    xBolinha += velocidadeXBolinha;
    yBolinha += velocidadeYBolinha;
  }

  function verificaColisaoBorda(){
    if (xBolinha + raio > width || xBolinha - raio < 0) {
    velocidadeXBolinha *= -1;
  }
    if (yBolinha +raio > height || yBolinha - raio < 0) {
    velocidadeYBolinha *= -1;
  }
}
  function mostraRaquete(x, y){
    rect(x, y, raqueteComprimento, raqueteAltura);
  }
  
  function movimentaMinhaRaquete(){
    if (keyIsDown(UP_ARROW)){
      yRaquete -=10;
    }
    if (keyIsDown(DOWN_ARROW)){
      yRaquete +=10;
    }
 
  }
  function movimentaRaqueteOponente(){
    velocidadeYOponente = yBolinha - yRaqueteOponente - raqueteComprimento / 2 - 30;
    yRaqueteOponente += velocidadeYOponente
    
  }
  
function verificaColisaoRaquete(x, y){
    colidiu = collideRectCircle(x, y, raqueteComprimento, raqueteAltura, xBolinha, yBolinha, raio)
    if (colidiu){
      velocidadeXBolinha *= -1;
      raquetada.play();
    }
  }
  
  function incluiPlacar(){
    stroke(255);
    textAlign(CENTER);
    textSize(16);
    
    fill(color(128,128,128));
    rect (150, 10, 40, 20);
    
    fill (255);
    text (meusPontos, 170, 26);
    
    fill(color(128,128,128));
    rect (450, 10, 40, 20);
    
    fill (255);
    text (pontosOponentes, 470, 26);
  }
  function marcaPonto(){
    if (xBolinha > 590){
      meusPontos += 1;
      ponto.play();
    }
    if (xBolinha < 10){
      pontosOponentes += 1;
      ponto.play();
    }
  }

