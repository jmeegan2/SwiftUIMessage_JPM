# SwiftUIMessage

`SwiftUI` wrapper of [MessageUI](https://developer.apple.com/documentation/messageui).

Always be sure to call `MailComposeView.canSendMail()` and `MessageComposeView.canSendText()` in-line to confirm that you can actually use them on that device. And graphical glitches may occur if you don't include the `.ignoresSafeArea()` view modifier.

It's generally best to use them in a `.sheet()` modifier, but the code below is just for the sake of example.

## MailComposeView
```swift
// This will return false if the device cannot use Apple Mail.
if MailComposeView.canSendMail() {
    MailComposeView(
        .init(subject: "Subject",
              toRecipients: [
                  "dummy@gmail.com"
              ],
              ccRecipients: nil,
              bccRecipients: nil,
              body: "This is an example email body.",
              bodyIsHTML: false,
              preferredSendingEmailAddress: nil)
    )
    .ignoresSafeArea()
} else {
    // Here you can tell the user the issue, or maybe launch the URL scheme to open the default mail app (which wouldn't be Apple Mail).
    Text("Mail cannot be sent from your device.")
}
```

## MessageComposeView
```swift
if MessageComposeView.canSendText() {
    MessageComposeView(
        .init(recipients: [
                  "111-111-1111",
                  "+1-111-111-1112"
              ],
              subject: "This is an MMS subject line, but it won't be inlcuded if the device doesn't have them enabled.",
              body: "This is an SMS text body.")
    )
    .ignoresSafeArea()
} else {
    // Here you can tell the user the issue.
    Text("Text messages cannot be sent from your device.")
}
```
