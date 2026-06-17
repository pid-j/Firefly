# Firefly

The assets for Firefly, a [TurboWarp](https://github.com/TurboWarp/) based operating system and its kernel, Lightning.

## What does this branch fix?

This branch includes some bug fixes for Lightning Varsovia. PB2 isn't fully fleshed out, and I understand that it's still in beta. With that in mind, here's what I fixed:
* Asking for password without a set password: This is something I didn't need to fix, but I wanted to fix it because it kept annoying me!!! I don't have a password!!1!!!!1!!111!
* Bugs in object conversion: When using the `IOBtoJSON` or `JSONtoIOB` commands, you could freeze the system or inject HTML/CSS/JS into the terminal. Some bugs I found (all of these were in the `Lightning APIs//Object Conversion` sprite) were:
  * The `JSONtoIOB` function would return InterObjects without proper escaping; it did not replace `|` with `||`, which is important because the pipe character is used as the escape character due to the backslash being used for separators.
  * The `lightning: parse iob (iob)` block could get stuck in a loop if the input was malformed (i.e: the input did not terminatse with a backslash). The block only checks for the input ending after the entire operation (fetch key and value) is completed; due to this, if the input did not end with a backslash, the index would keep increasing without checking if the character was empty.
  * Due to the way the Object Conversion API would write to the terminal, you could inject HTML/CSS/JS by using InterObjects or JSON with HTML code in them. This is fixed by using the HTML Encode block.

## What will happen to the branch?

I won't keep updating this branch as it'll probably get merged into the main Firefly repo.

## I don't understand, is there a demo?

Here's a demonstration on the original PB2:

https://github.com/user-attachments/assets/421a84c6-1a7a-4304-b5cc-a427d2c903c7

And now, here's a demonstration of PB2 with the above fixes:

https://github.com/user-attachments/assets/3b94bde7-504b-4c9f-9d4f-1b08586b3d04
