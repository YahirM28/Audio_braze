  
    <script>
document.addEventListener("click", function () {
  const audio = document.getElementById("bgAudio");
  audio.play();
}, { once: true });
</script>


<audio id="bgAudio" loop>
  <source src="images/audio.mp3" type="audio/mpeg">
</audio>
