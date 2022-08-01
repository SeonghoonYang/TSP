# TSP-project


### ATT dataset (att48, att532)
![att48](https://user-images.githubusercontent.com/55279227/182185157-dc94fb20-5296-4b0a-ad55-8bd72c2c93cf.gif)
![att532](https://user-images.githubusercontent.com/55279227/182188238-963dd122-5f9a-4816-9582-b2db3f30c3d5.gif)

#### CPU intel i7-2700 (3.5ghz)

att48 takes 5 minutes  ||   att532 takes 98 minutes

```python
  # prepare x, y pos list (n by 2) [[0, 0], [2, 3.2] ... ]
  file_name = 'att48'
  coords = []
  with open(file_name + '.txt') as f:
      for line in f.readlines():
          coords.append(list(map(float, [line.split()[-2], line.split()[-1]])))

  # prepare Euclidian distance table
  # [[0, 1, 3]
  #  [1, 0, 7]
  #  [3, 7, 0]] ... 
  coord_dist = [[((coords[i][0] - coords[j][0]) ** 2 + (coords[i][1] - coords[j][1]) ** 2) ** 0.5 
    for j in range(len(coords))] for i in range(len(coords))]
    
  tsp_obj = TSP(coords, coord_dist)
  tsp_obj.run(tsp_n=17, division_bound=5, path_tsp_n=12)
```
### This project finds quite short TSP path in a short time.
Using TSP(DP), path-TSP(Backtracking), k-means clustering algorithms. 

### run function parameter
1. tsp_n: TSP(DP) bound. recommend < 25
2. division_bound: number of cities of clusters. less is maybe better
3. path_tsp_n : path-TSP(Bruteforce with backtracking). more is better, recommend < 13  


```python
  # draw plot
  # path = [1, 7, 0, ...]
  # pos = [[0, 0], [2, 3] ...]
  # dist = int
  # color='royalblue'
  draw_path(tsp_obj.final_path, coords, tsp_obj.final_dist, color='r', dot=True)
  
  make_gif(tsp_obj=tsp_obj, file_name=file_name, coords = coords, dot=True, interval=0.1)
```
