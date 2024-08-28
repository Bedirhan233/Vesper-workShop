itch.io: https://yrgo-game-creator.itch.io/vesper
# Vesper - My work


Hello! I am happy to tell you that I have worked in Vesper with a great team!


<img src="https://github.com/Bedirhan233/Vesper-workShop/assets/114574131/b2fe0384-8a84-4781-8829-8a9ea26fba74" width="556,5" height="314,5">

<img src="https://github.com/Bedirhan233/Vesper-workShop/assets/114574131/74938797-5f8f-42ee-8c22-0d78424b5213" width="559,5" height="314">


I was one of the programmers, and my role was to handle all raycast systems in the game. It was grea
t because I enjoy creating logic for raycasts! Besides raycasting, I also had the responsibility to implement all audio for the game, make some juice implementations and of course bugfixing.

## Raycast system
Because our game involved a cube that changed size, we needed to create logic to prevent size changes in certain areas of the game. That's why I decided that a raycast system would be perfect for it. I kept it very basic and simple. I created a function that could send how many raycasts I wanted, vertically or horizontally, and if any of them hit something, a boolean value would be sent to another script to stop the size change. At the begining the system worked fine when we had a simple game and levels. However as the game and levels became more advanced, I got problems with my logic. First, I added functionality for diagonal angles too and then in some places we needed only one raycast to trigger the boolean, not all of them. Implementing the diagonal angle was not too complicated, but sending information about just one raycast proved to be challenging. My big mistake here was trying to implement all the logic into one function, making it very complicated and unreadable. That's when I decided to separate those functions, which worked better. From that point on, I added other functions instead of pressing everything into just one. This was the first time I had worked with raycasting in such a large game. Looking back, I realize I could have done things differently. For example, instead of just sending a single raycast, I could have used a raycast sphere to check the surroundings, or as I mentioned earlier, separated the logic into different functions. But I learned a lot about raycast logic from this project, and it was so fun to work with it.

Here is the function for it.
<details>
  <summary>Click to expand</summary>
  
```c#
bool RayCastGenerator(float characterSize, Vector2 direction, int totalRaycast)
{

    Vector2 startPos;

    Vector2 rightTop = new Vector2(1, 1);
    Vector2 rightDown = new Vector2(1, -1);
    Vector2 leftDown = new Vector2(-1, -1);
    Vector2 leftTop = new Vector2(-1, 1);


    bool canChangeSize = true;

    for (int i = 0; i < totalRaycast; i++)
    {
        if (direction == Vector2.up || direction == Vector2.down)
        {
            startPos = CalculatingRayStartPos(totalRaycast, i, true);

            centerRaycast = Physics2D.Raycast(startPos, direction, characterSize, mask);
            Debug.DrawRay(startPos, direction * characterSize, Color.red);
        }

        else if (direction == Vector2.right || direction == Vector2.left)
        {
            startPos = CalculatingRayStartPos(totalRaycast, i, false);

            centerRaycast = Physics2D.Raycast(startPos, direction, characterSize, mask);
            Debug.DrawRay(startPos, direction * characterSize, Color.red);
        }
        else if (direction == rightTop || direction == rightDown || direction == leftTop || direction == leftDown)
        {
            startPos = CalculatingRayStartPos(totalRaycast, i, false);

            centerRaycast = Physics2D.Raycast(startPos, direction, characterSize, mask);
            Debug.DrawRay(startPos, direction * characterSize, Color.red);
        }

        if (centerRaycast.collider != null)
        {
            return false;
        }
    }
    return canChangeSize;
}
```
</details>
Here you can see what my raycasts looked like.



![GIF 2024-04-14 17-37-43](https://github.com/Bedirhan233/Vesper-workShop/assets/114574131/955393f1-8dd8-4ea0-8d3e-e239193f4d39)



![size](https://github.com/Bedirhan233/Vesper-workShop/assets/114574131/f586583f-0a79-4000-9d14-ea5cf66b7afe)

All colors except red are used for other logic checks. For example, auto-climb to help the player.

itch.io: https://yrgo-game-creator.itch.io/vesper

  

  

