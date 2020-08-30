# general / Bases

> Points: 100

## Question

> What does this `bDNhcm5fdGgzX3IwcDM1` mean? I think it has something to do with bases.

### Hint

> Submit your answer in our competition's flag format.
> For example, if you answer was 'hello', you would submit 'picoCTF{hello}' as the flag.

## Solution

The clue `bases` sends us looking for an encoding method that uses a higher base.
Base64 comes to mind.
Putting the text through a base64 decoder reveals the flag.

### Flag

`picoCTF{l3arn_th3_r0p35}`
