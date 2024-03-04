<details>
  <summary>RaycastGenerator</summary>
  
```CS

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

private Vector2 CalculatingRayStartPos(int totalRaycast, int i, bool isHorizontal)
{
    Vector2 center = new Vector2(transform.position.x, transform.position.y);
    Vector2 startPos;

    if (isHorizontal)
    {
        scaleBetweenRaycasts = (col.bounds.size.x * distanceFromCenter) / totalRaycast;
        startPos = center + new Vector2((i - (totalRaycast - 1) / 2f) * scaleBetweenRaycasts, 0);
        return startPos;
    }
    else 
    {
        scaleBetweenRaycasts = (col.bounds.size.y * distanceFromCenter) / totalRaycast;
        startPos = center + new Vector2(0, (i - (totalRaycast - 1) / 2f) * scaleBetweenRaycasts);
        return startPos;
    }
   
}
