Reading Page

If you are not drafting a question:
  - List of questions downloaded from the server
    - Each question has the ability to be Upvoted, Shared, Answered, or Flagged/Reported as buttons shown below the question text
    - An answer status shown in the top left 
    - The number of upvotes and a % displayed
  - Search frame (Appears after clicking the Search Icon in the toolbar) - toggleable
    - Search bar 
    - Button for filters that takes you to the Advanced Search Filter Page
  - Draft button (Image of  the wireframe kangaroo)
    - Sends the user to the QuestionDrafting Page after popping back to the main page. This operation needs to be done on the main thread, since the main thread is also       the UI thread. Due to using async/await in the navigation process it could be trying to move these operations to other threads, but it needs to be done on main.
    - https://docs.microsoft.com/en-us/xamarin/essentials/main-thread#:~:text=This%20thread%20is%20often%20called,on%20the%20application's%20main%20thread.

If you are drafting a question, and additional frame shows up:
  - Draft Question Entry that holds your existing question draft text (if applicable)
  - Button to discard draft
  - Button to Keep the question and proceed to the question details page to review before uploading.
