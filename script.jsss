const holes = document.querySelectorAll('.hole');
const scoreBoard = document.querySelector('.score');
const moles = document.querySelectorAll('.mole');
const countdownBoard = document.querySelector('.countdown');
const startButton = document.querySelector('.startButton');
const highScoreBoard = document.querySelector('.highScore')

let lastHole;
let timeUp = false;
let timeLimit = 20000;
let score = 0;
let countdown;
let highScore = localStorage.getItem('game1HighScore') || 0;

function pickRandomHole() {
    const randomHole = Math.floor(Math.random() * holes.length)
    const hole = holes[randomHole]
    if(hole === lastHole) {
       return pickRandomHole(hole)
    }
    lastHole = hole;    
    return hole;
}

function popOut(holes) {
    const time = Math.random() * 1300 + 400;
    const hole = pickRandomHole(holes);
    hole.classList.add('up');
    setTimeout(function(){
        hole.classList.remove('up');
        if(!timeUp) popOut();
    }, time);
}

function startGame() {
    countdown = timeLimit/1000;
    scoreBoard.textContent = 0;
    scoreBoard.style.display ='block';
    countdownBoard.textContent = countdown;
    timeUp = false;
    score = 0;
    popOut();
    setTimeout(function(){
        timeUp = true;
    },timeLimit)
    
    let startCountdown = setInterval(function(){
        countdown -= 1;
        countdownBoard.textContent = countdown;
        if(countdown < 0) {
            countdown = 0;
            clearInterval(startCountdown);
            checkHighScore();
            countdownBoard.textContent = 'Times UP! Stay Safe!!'
        }    
    }, 1000)
}

startButton.addEventListener('click', startGame)

function whack(e) {
    score++;
    this.style.backgroundImage = 'url("monster1.jpg")'
    this.style.pointerEvents = 'none';
    setTimeout(() => {
        this.style.backgroundImage = 'url("virus-4930122_1920.png")'
        this.style.pointerEvents = 'all';
    }, 800)
    scoreBoard.textContent = score;
}
moles.forEach(mole => mole.addEventListener('click', whack))

function checkHighScore() {
    if (score > localStorage.getItem('getHighScore')) {
        localStorage.setItem('game1HighScore', score);
        highScore = score;
        highScoreBoard.textContent = 'HIGH SCORE: ' + highScore;
    }
}

let myInterval = -1;
let time = 0;
let title = document.getElementById('title')
const pauseBtn = document.getElementById('pause');
pauseBtn.addEventListener('click', (e) => {
    if(myInterval == -1) {
        pauseBtn.innerHTML ="Pause";
        myInterval = setInterval(function() {
            time ++;
            title.innerHTML = time;
        }, 1000);
    } else {
        pauseBtn.innerHTML = "Start";
        clearInterval(myInterval);
        myInterval = -1;
    }
})