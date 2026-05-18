# Group_F

|    NRP     |           Nama             |
| :--------: |       :------------:       |
| Aqilah Ibrahim           | 5025251260   |
| Valian Athalla Syahputra | 5025251156   |
| Rizqi Arya Kuskhilbyano  | 5025251161   |
| Athar Rozy Rasyidan      | 5025251009   |

MST Problem Island Hopping

### PROBLEM

You are a contractor for the small independent nation of Microisles, which is far out in the Pacific ocean, and made up of a large number of islands. The islanders travel between islands on boats, but the government has hired you to design a set of bridges that would connect all the islands together. However, they want to do this at a minimum cost. Cost is proportional to bridge length, so they want to minimize the total length of all bridges put together. You need to decide which bridges should connect which islands.

### INPUT

The first line contains an integer. After that, cases follow. Each case starts with a line containing the integer number of islands, followed by lines each containing the real-valued horizontal and vertical position of a bridge endpoint for the corresponding island. All bridge endpoints are, of course, unique. Each coordinate is in the range to meters and has at most digits past the decimal point.

### OUTPUT

For each test case, output the total length of bridges needed to connect all the islands accurate to relative and absolute error of 10^-3 meters.

### FULL CODE

```
#include <stdio.h>
#include <math.h>

struct pos
{
    double x, y;
};

double distance_squared(struct pos a, struct pos b)
{
    double dx = a.x - b.x;
    double dy = a.y - b.y;

    return dx * dx + dy * dy;
}

void test_case()
{
    int v;
    scanf("%d", &v);

    struct pos vertices[v];

    for (int i = 0; i < v; i++) //
    {
        scanf("%lf %lf", &vertices[i].x, &vertices[i].y);
    }

    int visited[v];
    double min_dist[v];

    for (int i = 0; i < v; i++)
    {
        visited[i] = 0;
        min_dist[i] = 1e18;
    }

    min_dist[0] = 0;

    double total = 0.0;

    for (int i = 0; i < v; i++)
    {
        int next = -1;

        for (int j = 0; j < v; j++)
        {
            if (!visited[j] &&
               (next == -1 || min_dist[j] < min_dist[next]))
            {
                next = j;
            }
        }

        visited[next] = 1;
        total += sqrt(min_dist[next]);

        for (int j = 0; j < v; j++)
        {
            if (!visited[j])
            {
                double dist = distance_squared(vertices[next], vertices[j]);

                if (dist < min_dist[j])
                {
                    min_dist[j] = dist;
                }
            }
        }
    }

    printf("%.3lf\n", total);
}

int main()
{
    int test_cases;
    scanf("%d", &test_cases);

    while (test_cases--)
    {
        test_case();
    }

    return 0;
}
```






