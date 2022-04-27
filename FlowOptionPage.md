# FlowOptionPage
  ![AnswerQuestionPage](https://user-images.githubusercontent.com/17503398/165642294-dd66af71-060f-4a32-a1ea-921dadfea61d.PNG)

## Elements:
  - 2 large boxes stacked on top of each other to determine 1 of the 2 main ways to navigate through the main question drafting flow of the application.
    
    You either:
    A. Make a question for the purpose of being public in the app and have an MP answer it
    or 
    B. Make a question that you'd like to be raised in Parliament
    
    - Each box consits of:
      - A frame to hold the inner contents
      - A main heading label
      - A subtext label to describe and elaborate on the main heading label
      - Two separate buttons to pick for who should answer your question.
      
  - The upper option's buttons navigate an MP ExploringPage to choose an MP to answer your question and then returns you to the ReadingPage
  - The lower box's button options navigates to either an MP ExploringPage or a Public Authority ExploringPage
    and then returns the user to the QuestionAskerPage to determine who should raise your question before going to the ReadingPage.
  
  - The page has a home button on the toolbar to bail out of the main flow of the question drafting process and return to the main page.

## ViewModel:
  - Makes use of the **QuestionViewModel.Instance** as part of the *"MainFlow"* for drafting questions
