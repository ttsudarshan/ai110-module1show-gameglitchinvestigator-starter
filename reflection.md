# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

The first time I ran the game, it showed a simple “Guess a number between 1 and 100” interface with an attempts counter and some buttons like New Game, difficulty options, hints, and developer info. I noticed that after my first guess, the remaining attempts number on the UI did not decrease, even though the game actually ended after I used what looked like my “last” attempt. I also saw that the New Game button didn’t actually restart the game, so I had to refresh the whole app to play again. The difficulty setting was clearly broken, because even on easier modes the app still asked me to guess numbers outside the supposed range. On top of that, the hint system was backwards or misleading, and the developer info/history section didn’t update to show the latest round.

---

## 2. How did you use AI as a teammate?

Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
I used Claude as my main AI coding assistant for this project. It helped me reason about bugs in the Streamlit app and suggested changes to the game logic and session state.

Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
Claude correctly suggested that I should move the secret number and remaining attempts into st.session_state instead of recomputing them on every run. After making that change, I rebuilt and ran the app multiple times, playing full games to confirm that the secret number stayed stable and the attempts counter decreased correctly on each guess.

Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).
At one point, Claude suggested generating a new random secret number inside the same block of code that handled each guess, which would have changed the number after every attempt.

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
 I considered a bug “really fixed” only after I could reproduce the original problem, apply my change, and then repeat the same steps without seeing the bad behavior again.

Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
One test I ran was `test_guess_too_high()` using pytest. In this test, the secret number was set to 50 and the guess was 60. The expected result was `"Too High"`. When I ran the test using `pytest`, it verified whether the `check_guess()` function correctly identified that a guess greater than the secret number should return `"Too High"`. This test helped confirm that the comparison logic in my function was working correctly and that the hints given to the player matched the expected behavior.

- Did AI help you design or understand any tests? How?

AI helped me understand how to structure unit tests using pytest and how to think about different scenarios the function should handle, such as a correct guess, a guess that is too high, and a guess that is too low. It also helped me verify that the order of parameters in the function (`guess` and `secret_number`) matched the test cases. By using AI, I was able to better understand how tests validate program logic and ensure that the guessing game behaves correctly.

---

## 4. What did you learn about Streamlit and state?

- In your own words, explain why the secret number kept changing in the original app.
- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
- What change did you make that finally gave the game a stable secret number?

The secret number kept changing because Streamlit reruns the entire script every time a user clicks a button or interacts with the app. In Streamlit, this means normal variables reset each time, so you need to store important values in `st.session_state`, which works like memory that keeps data between reruns. I fixed the problem by saving the secret number in `st.session_state` so it stays the same until the player starts a new game.


---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.

One habit I want to reuse in future projects is writing small tests with `pytest` to verify that my logic works correctly before integrating it into the main program. Next time I work with AI on a coding task, I would test the generated code more carefully and review the logic instead of assuming it works correctly. This project showed me that AI-generated code can be helpful for getting started, but it still needs careful debugging and verification by the programmer.
