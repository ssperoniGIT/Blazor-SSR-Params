This is a Blazor Static SSR project, with available interactive components. It uses:
builder.Services.AddRazorComponents() .AddInteractiveServerComponents();
The requirements are: The pages are all non-interactive (EditForms with submit). The project cannot have globally available interactivity (such as Blazor Server).
On many pages, we want to include an interactive component.
This test page is attempting to determine how to send a parameter (UserID) to the interactive components.
In this example, the child component is called: 'ChildInteractive'.
When a noninteractive page includes an interactive componant, Blazor will not let you use the standard method of including a parameter such as: ChildInteractive userid="aaa" ChildInteractive.
The solution seems to be that Cascading Parameters can be set in Program.cs that are available to all components, using:
builder.Services.AddCascadingValue("UserID", sp => (string)"Initial value, set in Program.cs");
(BTW, in a Static SSR project, Cascading Parameters set in Routes.razor are only available to non-interactive components.)
My question is: once the cascading parameter is set using builder.Services.AddCascadingValue, how do you modify the value? The use case is: all components (interactive and non-interactive) need to know the UserID. However, the UserID is not known until the user logs in. Once the user logs in, the cascading parameter, UserID, needs to be updated.

