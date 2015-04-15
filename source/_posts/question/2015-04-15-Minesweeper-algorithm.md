---
layout: post
title: "[Question] Minesweeper Algorithm "
comments: true
category: Question

---

### Question

> write a minesweeper algorithm with O(1) space usage

> Input matrix is represented with 1 (mine) and 0(vacant space). Return true if all 0s are connected.

  // 0 0 1
  // 0 1 0 ==> true
  // 0 0 0

  // 0 0 1
  // 0 1 0 => false
  // 1 0 0

### Solution

We essentially will travel through the entire 0s-connected area. The first time we visit a node, we mark the node as "2". The second time we visit, we mark it as "3". If the end, check if all "0" are marked as 2.

#### Example

Given this input:

    0 0 0 1 0
    0 1 1 1 1
    0 0 0 0 1
    0 1 1 0 1
    0 0 1 0 1

The step by step illustration:

    Step #1
    2 0 0 1 0
    0 1 1 1 1
    0 0 0 0 1
    0 1 1 0 1
    0 0 1 0 1

    Step #2
    2 0 0 1 0
    2 1 1 1 1
    0 0 0 0 1
    0 1 1 0 1
    0 0 1 0 1

    Step #3
    2 0 0 1 0
    2 1 1 1 1
    2 0 0 0 1
    0 1 1 0 1
    0 0 1 0 1

    Step #4
    2 0 0 1 0
    2 1 1 1 1
    2 0 0 0 1
    2 1 1 0 1
    0 0 1 0 1

    Step #5
    2 0 0 1 0
    2 1 1 1 1
    2 0 0 0 1
    2 1 1 0 1
    2 0 1 0 1

    Step #6
    2 0 0 1 0
    2 1 1 1 1
    2 0 0 0 1
    2 1 1 0 1
    2 2 1 0 1

    Step #7
    2 0 0 1 0
    2 1 1 1 1
    2 0 0 0 1
    2 1 1 0 1
    2 3 1 0 1

    Step #8
    2 0 0 1 0
    2 1 1 1 1
    2 0 0 0 1
    2 1 1 0 1
    3 3 1 0 1

    Step #9
    2 0 0 1 0
    2 1 1 1 1
    2 0 0 0 1
    3 1 1 0 1
    3 3 1 0 1

    Step #10
    2 0 0 1 0
    2 1 1 1 1
    2 2 0 0 1
    3 1 1 0 1
    3 3 1 0 1

    Step #11
    2 0 0 1 0
    2 1 1 1 1
    2 2 2 0 1
    3 1 1 0 1
    3 3 1 0 1

    Step #12
    2 0 0 1 0
    2 1 1 1 1
    2 2 2 2 1
    3 1 1 0 1
    3 3 1 0 1

    Step #13
    2 0 0 1 0
    2 1 1 1 1
    2 2 2 2 1
    3 1 1 2 1
    3 3 1 0 1

    Step #14
    2 0 0 1 0
    2 1 1 1 1
    2 2 2 2 1
    3 1 1 2 1
    3 3 1 2 1

    Step #15
    2 0 0 1 0
    2 1 1 1 1
    2 2 2 2 1
    3 1 1 2 1
    3 3 1 3 1

    Step #16
    2 0 0 1 0
    2 1 1 1 1
    2 2 2 2 1
    3 1 1 3 1
    3 3 1 3 1

    Step #17
    2 0 0 1 0
    2 1 1 1 1
    2 2 2 3 1
    3 1 1 3 1
    3 3 1 3 1

    Step #18
    2 0 0 1 0
    2 1 1 1 1
    2 2 3 3 1
    3 1 1 3 1
    3 3 1 3 1

    Step #19
    2 0 0 1 0
    2 1 1 1 1
    2 3 3 3 1
    3 1 1 3 1
    3 3 1 3 1

    Step #20
    2 0 0 1 0
    2 1 1 1 1
    3 3 3 3 1
    3 1 1 3 1
    3 3 1 3 1

    Step #21
    2 0 0 1 0
    3 1 1 1 1
    3 3 3 3 1
    3 1 1 3 1
    3 3 1 3 1

    Step #22
    2 2 0 1 0
    3 1 1 1 1
    3 3 3 3 1
    3 1 1 3 1
    3 3 1 3 1

    Step #23
    2 2 2 1 0
    3 1 1 1 1
    3 3 3 3 1
    3 1 1 3 1
    3 3 1 3 1

    Step #24
    2 2 3 1 0
    3 1 1 1 1
    3 3 3 3 1
    3 1 1 3 1
    3 3 1 3 1

    Step #25
    2 3 3 1 0
    3 1 1 1 1
    3 3 3 3 1
    3 1 1 3 1
    3 3 1 3 1

  Result is false

### Code

The following code is very-well commented, so just reading the code would give you a good idea of what I meant.

    public boolean validate(int[][] matrix, int m, int n) {
        Pos nextStep = findZero(matrix, m, n);
        if (nextStep == null) {
            // the matrix deos not contain 0
            return false;
        }

        // visit the first position, and go from there
        matrix[nextStep.x][nextStep.y] = 2;
        while (nextStep != null) {
            nextStep = step(matrix, nextStep, m, n);
        }

        // after visiting all positions, check if there is remaining 0s
        return findZero(matrix, m, n) == null;
    }

    Pos step(int[][] matrix, Pos cur, int m, int n) {
        // Now cur is located at a pos with value = 2
        // print matrix in "verbose" mode
        if (verbose) {
            System.out.println("Step #" + stepCount++);
            for (int[] array : matrix) {
                for (int num : array) {
                    System.out.print(num + " ");
                }
                System.out.println();
            }
            System.out.println();
        }

        // make a list of valid neighbors, for the convenience of checking
        List<Pos> neighbors = new ArrayList<Pos>();
        neighbors.add(new Pos(cur.x - 1, cur.y));
        neighbors.add(new Pos(cur.x + 1, cur.y));
        neighbors.add(new Pos(cur.x, cur.y - 1));
        neighbors.add(new Pos(cur.x, cur.y + 1));
        for (int i = neighbors.size() - 1; i >= 0; i--) {
            if (!isValidPos(neighbors.get(i), m, n)) {
                neighbors.remove(i);
            }
        }

        // check if there is adjacent 0,
        // if there is, mark 0 as 2 and return that position
        for (Pos neighbor : neighbors) {
            if (matrix[neighbor.x][neighbor.y] == 0) {
                matrix[neighbor.x][neighbor.y] = 2;
                return neighbor;
            }
        }

        // if no adjacent 0, then check if there is adjacent 2.
        // if there is, mark current as 3 and then return that position
        for (Pos neighbor : neighbors) {
            if (matrix[neighbor.x][neighbor.y] == 2) {
                matrix[cur.x][cur.y] = 3;
                return neighbor;
            }
        }

        //if no adjacent 0 and no adjacent 2, mark current as 3 and return null
        matrix[cur.x][cur.y] = 3;
        return null;
    }

    boolean isValidPos(Pos p, int m, int n) {
        return p.x >= 0 && p.x < m && p.y >= 0 && p.y < n;
    }

    Pos findZero(int[][] matrix, int m, int n) {
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (matrix[i][j] == 0) {
                    return new Pos(i, j);
                }
            }
        }
        return null;
    }

    class Pos {
        int x;
        int y;

        public Pos(int a, int b) {
            x = a;
            y = b;
        }
    }
