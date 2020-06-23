This builds on https://github.com/axmandm/sgdk-game-music to allow the game to be restarted if "Start" is pressed on the joypad.

Add a function to handle when Start is pressed on JOY_1, or if A is pressed.

```
void handleJoyEvent(u16 joy, u16 changed, u16 state)
{
    if (joy == JOY_1)
    {
        if (changed & ~state & BUTTON_START)
        {
            timer = 3;
            SYS_reset ();
        }
        if (changed & ~state & BUTTON_A)
        {
            timer = timer + 3;
        }

    }
}
```

Note that we reset the timer also, as otherwise the system will reset with the timer as 0.

Within the main loop, call:
`JOY_setEventHandler(handleJoyEvent);`
