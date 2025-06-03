# Swap Feature for [Tonkeeper](https://github.com/tonkeeper)'s Android app

### Repository contents

This repository is a fork of Tonkeeper X ([TON](https://ton.org) wallet, Kotlin-based Android app) that includes the following [changes](https://github.com/vkryl/tonkeeper-android/compare/main...vkryl:tonkeeper-android:contest-2024) for the [contest](https://t.me/tonkeeper_news/91) held in 2024:

* The Swap feature implementation that is based on the provided [static mockups](https://www.figma.com/file/8KdIRGt1dAmyMDW63Y8XBL/Tonkeeper-Contest-%C2%B7-iOS-%C2%B7-Android)
* UI animations and few features that are not included in any of the mockups
* Tools for simplifying building animations in the Android app
* Some widgets that could be re-used in other places of the app
* App bugfixes outside of contest scope, like proper displaying of balances (prior to this submission Tonkeeper X displayed incorrect token balances everywhere among the app).

🏆 This submission has earned the **🥇 1st place**. The only purpose of this repository is to preserve and showcase the achieved result.

Source code of the changes made to the original repository can be viewed [here](https://github.com/vkryl/tonkeeper-android/compare/main...vkryl:tonkeeper-android:contest-2024).

### Video demo

https://github.com/user-attachments/assets/8be13f7b-b1ed-446a-b055-5d19adc4d8ad

### Technical credits

I wanted to give an additional credit to some probably not noticeable things, but which required an effort, given the limited duration of the contest and zero project documentation available (the only available resources were the source code and static mockups):

1. Balances and rates displayed in the new `Swap` section are the only place in the app where they are displayed accurately. It turns out that balances that app displays in various places are not correct, because 32-bit `float` is used. 64-bit `signed long` for nano also causes problems for some tokens (`FISH` token is the best for finding all of the problems: when you open chart screen, where the balance is intended to be displayed accurately, many digits are zeroed out). I've deprecated some of the methods, added properly working alternatives, and added comments with guide on how to migrate to them in other parts of the app.

2. When entering swap screen (`Continue` button), the transaction is simulated on the blockchain, and up-to-date market rate is fetched.

3. Blockchain fee is displayed on confirmation screen instead of hadcoded string like in `tonkeeper.ston.fi`

4. App tries to show the difference in market price for swapping tokens (increases the decimal part until the difference is visible to user)

5. Transparent user-friendly error handling. For example, rate API behaves weirdly (e.g. for some wallets it doesn't return USDT rate), however, app transparently notifies the user at every step about any potential errors / outdated information.

6. Swap section properly handles different user currencies. It doesn't hardcode number of decimals, but calculates how big decimal part should be on the fly

7. Formatting and support for any locales in amount input: for EN/RU decimal and grouping separator characters are different. App properly handles them (and other locales too, if they ever come to Tonkeeper X)

8. RTL support: all new screens properly handle RTL direction just in case Arabic, Hebrew or Persian ever comes to Tonkeeper X

9. Network handling: if `Swap` screen is opened without network, or connection is lost while it was open, it will properly recover once the device is back online.

10. Made some optimizations and bugfixes outside of the Swap section, like for trimmed balances in the balances list

11. Easter egg: quick picker by holding choose token (re-used from send screen)