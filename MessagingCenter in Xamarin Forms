# Messaging Center

## Description:
MessagingCenter allows us to **publish/send** a message from one part of the code and receive it in another from a **subscriber/listener**.
They work independently of each other. With message publishers not needing to know of any pre-existing listeners, and similarly, subscribers not needing to
be aware of any extra potential senders. The only thing that each component cares about is the actual message string that is being sent or looked for to receive.

One of the neat things about the MessagingCenter is that it allows us to pass data to previous pages as well. Microsoft's .Net MAUI will implement a way to do this
but until upgrading to .Net MAUI from Xamarin.Forms the best way to pass data to previous pages in a form of "backwards navigation" is to utilize the MessagingCenter.

Currently you can pass data through pages by passing objects into their constructors, but instead of chaining object from pageA to pageB to pageC to pageD because 
pageD needed to know what was on pageA, and the only way to get to pageD from pageA was to go through B and C (but they don't need to use that data). 
You can skip passing it to the pages that don't need it by having the listener be on pageD and the sender send it from pageA to skip the middle few steps.

## How we utilize it:
We use MessagingCenter in the RightToAsk application as a way to indicate where we want to navigate to on future pages, based on which pages the user
has previously come from. In the app there are many ways in which the user can start creating an account. Depending on where they came from previously
determines where we would like to place them back into the flow of the application after finishing the account creation process
so that it appears as seamless as possible.

## Example Publisher:
MessagingCenter.Send(this, "MessageToSend"); // "this" is the instance of the ViewModel that the message is being sent from
// That line could also be written as the following
MessagingCenter.Send<NameOfViewModel>(this, "MessageToSend"); // though shorthand generally forgoes the <NameOfViewModel> part

## Example Subscriber:
MessagingCenter.Subscribe<NameOfViewModel>(this, "MessageToSend", (sender) =>
{
  // Do something here
  CameFromMainPage = true;
  // unsubscribe if you don't want to continually hit this listener / only hit it one time i.e. when the ViewModel this page is attached to is created
  MessagingCenter.Unsubscribe<NameOfViewModel>(this, "MessageToSend");
});
// here the name of the ViewModel in <> is supposed to be the ViewModel where you expect the message to be coming from.
// The "MessageToSend" is the incoming message you are looking for from that particular ViewModel location

## Example with Args:
// if you wish to pass an object with data along with the message, you may send it as an argument/parameter in the following manner
MessagingCenter.Send<NameOfViewModel, ObjectTypeToSend>(this, "MessageToSend", objectValueToSend);
Ex: 
MessagingCenter.Send<NameOfViewModel, bool>(this, "MessageToSend", true);
MessagingCenter.Subscribe<NameOfViewModel, bool>(this, "MessageToSend", (sender, arg) =>
{
  // Do something here
  var data = arg.ToString();
  // unsubscribe if you don't want to continually hit this listener / only hit it one time i.e. when the ViewModel this page is attached to is created
  MessagingCenter.Unsubscribe<NameOfViewModel>(this, "MessageToSend");
});

## Link To Microsoft Docs:
https://docs.microsoft.com/en-us/xamarin/xamarin-forms/app-fundamentals/messaging-center
