# Problem 733 - Flood Fill - Easy
An image is represented by an `m x n` integer grid `image` where `image[i][j]` represents the pixel value of the image.

You are also given three integers `sr`, `sc`, and `color`. You should perform a **flood fill** on the image starting from the pixel `image[sr][sc]`.

To perform a **flood fill**, consider the starting pixel, plus any pixels connected **4-directionally** to the starting pixel of the same color as the starting pixel, plus any pixels connected **4-directionally** to those pixels (also with the same color), and so on. Replace the color of all of the aforementioned pixels with `color`.

Return *the modified image after performing the flood fill*.

 

**Example 1:**

![Example1](733e1.jpg)

```
Input: image = [[1,1,1],[1,1,0],[1,0,1]], sr = 1, sc = 1, color = 2
Output: [[2,2,2],[2,2,0],[2,0,1]]
Explanation: From the center of the image with position (sr, sc) = (1, 1) (i.e., the red pixel), all pixels connected by a path of the same color as the starting pixel (i.e., the blue pixels) are colored with the new color.
Note the bottom corner is not colored 2, because it is not 4-directionally connected to the starting pixel.
```
**Example 2:**
```
Input: image = [[0,0,0],[0,0,0]], sr = 0, sc = 0, color = 0
Output: [[0,0,0],[0,0,0]]
Explanation: The starting pixel is already colored 0, so no changes are made to the image.
```

**Constraints:**

- `m == image.length`
- `n == image[i].length`
- `1 <= m, n <= 50`
- `0 <= image[i][j], color < 216`
- `0 <= sr < m`
- `0 <= sc < n`

---
## Solution - C++

### 12 ms, 14.1 mb

```
vector<vector<int>> floodFill(vector<vector<int>>& image, int sr, int sc, int color) {
        if(image[sr][sc] == color)
            return image;
        int m = image.size();
        int n = image[0].size();
        int ori_col = image[sr][sc];
        queue<pair<int, int>> queue_;
        image[sr][sc] = color;
        queue_.push({sr,sc});
          
        while(!queue_.empty()){
            pair<int, int> current;
            current = queue_.front();
            queue_.pop();
            int x = current.first;
            int y = current.second;
            
            if(x - 1 >= 0 && image[x-1][y] == ori_col){
                image[x-1][y] = color;
                queue_.push({x-1,y});
            }
            
            if(x + 1 < m && image[x+1][y] == ori_col){
                image[x+1][y]=color;
                queue_.push({x+1,y});
            }
            
            if(y - 1 >= 0 && image[x][y-1] == ori_col){
                image[x][y-1]=color;
                queue_.push({x,y-1});
            }
            
            if(y + 1 < n && image[x][y+1] == ori_col){
                image[x][y+1]=color;
                queue_.push({x,y+1});
            }
        }
        return image;
    }
```