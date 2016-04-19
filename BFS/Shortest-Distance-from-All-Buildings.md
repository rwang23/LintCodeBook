##Shortest Distance from All Buildings

	Total Accepted: 3537 Total Submissions: 11368 Difficulty: Hard
	You want to build a house on an empty land which reaches all buildings in the shortest amount of distance.
	You can only move up, down, left and right.
	You are given a 2D grid of values 0, 1 or 2, where:

	Each 0 marks an empty land which you can pass by freely.
	Each 1 marks a building which you cannot pass through.
	Each 2 marks an obstacle which you cannot pass through.
	For example, given three buildings at (0,0), (0,4), (2,2), and an obstacle at (0,2):

	1 - 0 - 2 - 0 - 1
	|   |   |   |   |
	0 - 0 - 0 - 0 - 0
	|   |   |   |   |
	0 - 0 - 1 - 0 - 0
	The point (1,2) is an ideal empty land to build a house,
	as the total travel distance of 3+3+1=7 is minimal. So return 7.

####思路
- BFS
- 设置一个Point[] = new Point[m * n],定义Point包含x,y,distance, isRoom
- 从每个Building来BFS,记录每个点到Building的距离,设置distance(表示到各个building的距离和),对每个Building进行BFS时,加进distance
- 然后遍历Point array,找到distance最小的Point.返回
