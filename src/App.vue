<script setup>
  import { ref } from "vue";
  var a = [[], [], []];
  var cur = "X";
  var cnt = 9;

  for (var i = 0; i < 3; ++i)
    for (var j = 0; j < 3; ++j)
      a[i][j] = ref('');

  const fill = (x, y) =>
  {
    if (a[x][y].value == "")
    {
      a[x][y].value = cur;
      if (cur == "X")
        cur = "O";
      else
        cur = "X";
      --cnt;
    }
  }

  const isWinner = (x, y) =>
  {
    if (check(x, y))
    {
      alert("Winner: " + a[x][y].value);
      cur = a[x][y].value;
      reset();
    }
    else if (cnt == 0)
    {
      alert("Draw!");
      reset();
    }
  }

  const reset = () =>
  {
    for (var i = 0; i < 3; ++i)
      for (var j = 0; j < 3; ++j)
        a[i][j].value = "";
    cnt = 9;
  }

  const check = (x, y) =>
  {
    console.log(x + " " + y);
    if (a[0][0].value != "" && a[0][0].value == a[1][1].value && a[1][1].value == a[2][2].value)
        return true;
    if (a[0][2].value != "" && a[0][2].value == a[1][1].value && a[1][1].value == a[2][0].value)
      return true;
    let ok = true;
    for (let i = 1; i < 3; ++i)
    {
      if (a[i][y].value != a[0][y].value)
      {
        ok = false;
        break;
      }
    }
    if (ok && a[0][y] != "")
      return ok;
    ok = true;
    for (let i = 1; i < 3; ++i)
    {
      if (a[x][i].value != a[x][0].value)
      {
        ok = false;
        break;
      }
    }
    return ok && a[x][0] != "";
  }
</script>

<template>
  <main>
    <div>
      <h1>Tic tac toe</h1>
      <table align="center">
        <tr>
          <td @click="fill(0, 0); isWinner(0, 0)">{{ a[0][0].value }}</td>
          <td @click="fill(0, 1); isWinner(0, 1)">{{ a[0][1].value }}</td>
          <td @click="fill(0, 2); isWinner(0, 2)">{{ a[0][2].value }}</td>
        </tr>
        <tr>
          <td @click="fill(1, 0); isWinner(1, 0)">{{ a[1][0].value }}</td>
          <td @click="fill(1, 1); isWinner(1, 1)">{{ a[1][1].value }}</td>
          <td @click="fill(1, 2); isWinner(1, 2)">{{ a[1][2].value }}</td>
        </tr>
        <tr>
          <td @click="fill(2, 0); isWinner(2, 0)">{{ a[2][0].value }}</td>
          <td @click="fill(2, 1); isWinner(2, 1)">{{ a[2][1].value }}</td>
          <td @click="fill(2, 2); isWinner(2, 2)">{{ a[2][2].value }}</td>
        </tr>
      </table>
      <br>
      <button @click="reset()">Restart!</button>
    </div>
  </main>
</template>

<style scoped>
  main
  {
    width: 100wh;
    height: 100vh;
    background-color: lightcyan;
    color: brown;
    font-family: monospace;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  div
  {
    text-align: center;
  }

  td
  {
    width: 150px;
    height: 150px;
    text-align: center;
    border: 5px solid black;
    font-size: 75px;
  }

  h1
  {
    font-size: 50px;
  }

  button
  {
    width: 150px;
    height: 50px;
    background-color: lightsalmon;
    color: white;
    border: 0px;
    font-size: 30px;
    font-family: monospace;
  }
</style>