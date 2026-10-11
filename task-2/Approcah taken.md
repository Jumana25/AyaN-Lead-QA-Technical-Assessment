### Exploration uncovered potentially serious issues, particularly financial integrity, data consistency, and session management.

> * The approach taken in this task was primarily exploratory.
>
> * I first created a user and started making some transactions.
>
> * **Transaction Issues**
    >
    >   * The first issue I noticed was that, despite receiving a transfer confirmation, the source account balance remained unchanged.
>   * I performed more transfers and noticed additional transactions that I hadn't initiated.
>
> * **Account and Data Issues**
    >
    >   * I logged out and created a new user to verify the issue, only to discover that my first user had disappeared from the system.
>   * I continued with the second user and added two accounts. I confirmed that the recipient's balance increased without any deduction from the source account, and then the system crashed.
>   * The next day, I tried logging in with my first user and, surprisingly, it worked.
>   * The only reproducible issue I found occurred when requesting a loan with a decimal value in the down payment, which caused multiple unexpected accounts to appear under my user.
>   * Currently, none of my test users appear to exist in the system.
>
> * **Session and User Data Isolation Issues**
    >
    >   * One additional scenario I explored involved logging in with both users in two browser windows, one of them in incognito mode.
>   * I copied User 1's `JSESSIONID`, replaced User 2's session ID with it, and refreshed the page.
>   * The second window displayed User 1's data. Afterward, User 1 could log in using User 2's credentials but still saw User 1's data.
>   * At one point, both users' sessions displayed the same accounts.
>
> * **Environment Stability**
    >
    >   * The major issue with this website, in my opinion, is that it is unstable for testing purposes. Despite reproducing the issue several times, the system crashed again when I tried to capture screenshots for my defect report.
