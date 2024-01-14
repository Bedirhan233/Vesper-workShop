<details>
  <summary>RaycastGenerator</summary>
  
```CS

bool RayCastGenerator(float characterSize, Vector2 direction, int totalRaycast, bool allOfThem = false)
{
    Vector3 center = new Vector3(transform.position.x, transform.position.y);

    bool canChangeSize = true;

    for (int i = 0; i < totalRaycast; i++)
    {

        if (direction == Vector2.up || direction == Vector2.down)
        {
            offset = (col.bounds.size.x * edgeOffset) / totalRaycast;
            centerRaycast = Physics2D.Raycast(center + new Vector3((i - (totalRaycast - 1) / 2f) * offset, 0), direction, characterSize, mask);
            Debug.DrawRay(center + new Vector3((i - (totalRaycast - 1) / 2f) * offset, 0), direction * characterSize, Color.red);
        }

        else if (direction == Vector2.right || direction == Vector2.left)
        {
            offset = (col.bounds.size.y * edgeOffset) / totalRaycast;
            centerRaycast = Physics2D.Raycast(center + new Vector3(0, (i - (totalRaycast - 1) / 2f) * offset), direction, characterSize, mask);
            Debug.DrawRay(center + new Vector3(0, (i - (totalRaycast - 1) / 2f) * offset), direction * characterSize, Color.red);
        }
        else if (direction == new Vector2(1, 1) || direction == new Vector2(1, -1) || direction == new Vector2(-1, 1) || direction == new Vector2(-1, -1))
        {
            offset = (col.bounds.size.y * edgeOffset) / totalRaycast;
            centerRaycast = Physics2D.Raycast(center + new Vector3((i - (totalRaycast - 1) / 2f), (i - (totalRaycast - 1) / 2f) * offset), direction, characterSize, mask);
            Debug.DrawRay(center + new Vector3((i - (totalRaycast - 1) / 2f), (i - (totalRaycast - 1) / 2f) * offset), direction * characterSize, Color.red);
        }




        if (centerRaycast.collider == null)
        {
            canChangeSize = true;
        }
        else
        {
            canChangeSize = false;
        }


    }

    return canChangeSize;

}
