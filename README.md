<style>
div.warn {
    background-color: #fcf2f2;
    border-color: #dFb5b4;
    border-left: 5px solid #dfb5b4;
    padding: 0.5em;
    }
 </style>

# Getting Started with Satellite 6 Command Line
>**NOTE**:
This book is UNFINISHED - I was waiting for a bug with hostgroup creation to be fixed, but then I found that also host creation doesnt work via hammer either.

>Ive decided to release the book anyway, I still think it has useful infromation in it

>I shall update the book, once the final bugs are resolved

----
In this, the second book in the series, we look at using Satellite 6's command line tool, called Hammer

While the web interface is very nice, its often more efficient to use the command line, especially as it enables scripting.

We shall again start of with focusing on configuring a freshly installed Satellite so that it can provision machines. We will use an "all in one" setup, where the Satellite box will also perform DNS, DHCP and TFTP

Many of the first steps are identical to those in the sister book **Getting Started with Satellite 6**, but we have included them here anyway
