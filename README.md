<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Lyrics Player</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@700&display=swap" rel="stylesheet">
<style>
  body {
    background: black;
    color: white;
    font-family: 'Poppins', sans-serif;
    text-align: center;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100vh;
    overflow: hidden;
  }
  #startButton {
    font-size: 2rem;
    padding: 15px 30px;
    background: #00ffcc;
    color: black;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    transition: opacity 0.5s ease;
  }
  #lyrics {
    font-size: 1.5rem;
    opacity: 0;
    transition: opacity 1s ease;
    min-height: 3em;
    margin-top: 20px;
    width: 90%;
  }
  #finalMsg {
    font-size: 1.5rem;
    opacity: 0;
    transition: opacity 1s ease;
    margin-top: 20px;
  }
</style>
</head>
<body>

<button id="startButton">▶ Play</button>

<!-- put your mp3 file here, e.g. FoolishOne.mp3 -->
<audio id="audio" src="FoolishOne.mp3"></audio>

<div id="lyrics"></div>
<div id="finalMsg">performative pala ah 😜 bleeee</div>

<script>
const startButton = document.getElementById('startButton');
const audio = document.getElementById('audio');
const lyricsDiv = document.getElementById('lyrics');
const finalMsg = document.getElementById('finalMsg');

// Fill with your own timestamps (seconds)
const lyrics = [
  { time: 0, text: "You know how to keep me waitin'" },
  { time: 5, text: "I know how to act like I'm fine" },
  { time: 10, text: "Don't know what to call this situation" },
  { time: 15, text: "But I know I can't call you mine" },
  { time: 20, text: "And it's delicate, but I will do my best to seem bulletproof" },
  { time: 25, text: "'Cause when my head is on your shoulder" },
  { time: 30, text: "It starts thinkin' you'll come around" },
  { time: 35, text: "And maybe, someday, when we're older" },
  { time: 40, text: "This is something we'll laugh about" },
  { time: 45, text: "Over coffee every mornin' while you're watching the news" },
  { time: 50, text: "But then the voices say, 'You are not the exception" },
  { time: 55, text: "You will never learn your lesson'" },
  { time: 60, text: "Foolish one" },
  { time: 65, text: "Stop checkin' your mailbox for confessions of love" },
  { time: 70, text: "That ain't never gonna come" },
  { time: 75, text: "You will take the long way, you will take the long way down" },
  // add more lines/time stamps here if needed
];

let currentLine = -1;

startButton.addEventListener('click', () => {
  startButton.style.opacity = 0;
  setTimeout(() => startButton.style.display = 'none', 500);
  audio.play();
});

audio.addEventListener('timeupdate', () => {
  const currentTime = audio.currentTime;
  for (let i = lyrics.length - 1; i >= 0; i--) {
    if (currentTime >= lyrics[i].time) {
      if (currentLine !== i) {
        currentLine = i;
        lyricsDiv.style.opacity = 0; // fade out
        setTimeout(() => {
          lyricsDiv.textContent = lyrics[i].text;
          lyricsDiv.style.opacity = 1; // fade in
        }, 500);
      }
      return;
    }
  }
});

audio.addEventListener('ended', () => {
  lyricsDiv.style.opacity = 0;
  setTimeout(() => {
    finalMsg.style.opacity = 1;
  }, 500);
});
</script>

</body>
</html>
