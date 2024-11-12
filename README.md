<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Wedding Countdown</title>
    <!-- Add Google Fonts -->
    <link
      href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@600&family=Dancing+Script:wght@500&display=swap"
      rel="stylesheet"
    />
    <style>
      body {
        font-family: "Playfair Display", serif;
        background-color: #fbf8f4;
        color: #a67b5b;
        margin: 0;
        padding: 0;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
      }

      .countdown-container {
        text-align: center;
        background-color: #fffaf2;
        padding: 20px;
        border: 2px solid #e0dcd5;
        border-radius: 10px;
        box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
        width: 80%;
        max-width: 500px;
      }

      h1 {
        font-family: "Dancing Script", cursive;
        font-size: 2.5em;
        font-weight: 500;
        margin-bottom: 10px;
        color: #8c6954;
      }

      #timer {
        font-size: 1.3em;
        font-weight: 400;
        margin-top: 10px;
        color: #8c6954;
      }

      #date-input {
        margin: 20px 0;
      }

      input[type="date"] {
        font-size: 1em;
        padding: 10px;
        width: 100%;
        max-width: 300px;
        border: 1px solid #a67b5b;
        border-radius: 5px;
        color: #a67b5b;
        background-color: #fbf8f4;
        margin-bottom: 10px;
      }

      button {
        font-family: "Playfair Display", serif;
        font-size: 1.1em;
        font-weight: 600;
        padding: 10px 20px;
        border: none;
        border-radius: 5px;
        background-color: #a67b5b;
        color: white;
        cursor: pointer;
        box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
      }

      button:hover {
        opacity: 0.9;
      }

      /* Styling for timer to look like the image */
      .highlight {
        font-size: 1.1em;
        font-weight: bold;
        color: #8c6954;
      }
    </style>
  </head>
  <body>
    <div class="countdown-container">
      <h1>Wedding Day</h1>
      <div id="date-input">
        <input type="date" id="target-date" />
        <button id="start-button">Start Countdown</button>
      </div>
      <div id="timer">Select a date to begin the countdown.</div>
    </div>

    <script>
      let interval; // Declare interval globally

      document
        .getElementById("start-button")
        .addEventListener("click", function () {
          const targetDateInput = document.getElementById("target-date").value; // Get date input
          const timer = document.getElementById("timer");

          if (!targetDateInput) {
            timer.innerHTML = "Please select a valid date!";
            return;
          }

          const targetDate = new Date(targetDateInput).getTime();

          // Hide the date input and button
          document.getElementById("date-input").style.display = "none";

          // Clear existing countdown (if any)
          clearInterval(interval);

          function updateTimer() {
            const now = new Date().getTime();
            const distance = targetDate - now;

            if (distance <= 0) {
              timer.innerHTML = `<span class="highlight">It's time!</span>`;
              clearInterval(interval);
              return;
            }

            const weeks = Math.floor(distance / (1000 * 60 * 60 * 24 * 7));
            const days = Math.floor(
              (distance % (1000 * 60 * 60 * 24 * 7)) / (1000 * 60 * 60 * 24)
            );
            const hours = Math.floor(
              (distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)
            );
            const minutes = Math.floor(
              (distance % (1000 * 60 * 60)) / (1000 * 60)
            );
            const seconds = Math.floor((distance % (1000 * 60)) / 1000);

            timer.innerHTML = `
          <span class="highlight">${weeks}w</span> 
          <span class="highlight">${days}d</span> 
          <span class="highlight">${hours}h</span> 
          <span class="highlight">${minutes}m</span> 
          <span class="highlight">${seconds}s</span> to go
        `;
          }

          // Update timer immediately and every second
          updateTimer();
          interval = setInterval(updateTimer, 1000);
        });
    </script>
  </body>
</html>
