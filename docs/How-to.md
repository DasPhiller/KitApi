# How to

Here, I want to show you how to install the API

> **It's available for Paper 1.20.1**
>
> In order to use this API you need to use the Paper API 1.20.1 as well.
>
{style="note"}

## Before you start

The implementations you need are.

Make sure that:
- net.axay:kspigot:1.20.1
- paperDevBundle for 1.20.1

are installed


## Install the API

Then you download the kitapi jar from [github](https://cdn.discordapp.com/attachments/892367568432668693/1163572466216620203/kitapi-0.1.0.jar?ex=6540104e&is=652d9b4e&hm=35692f95a75af3f09893a95f3d5413b5e85b7bd1bba2dfac7dc6e833c82ef97e&)
and put it in your Projects libs folder 
> If there is no libs folder, create one
>
{style="note"}
1. implement it in your build.gradle.kts

   ```Gradle
    implementation(files("libs/kitapi-0.1.0.jar")
   ```
