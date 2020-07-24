<script>
import { getContext } from 'svelte'
const context = getContext('swipeable')
const progress = $context.progress
$: currentIndex = Math.floor($progress + 0.5)
</script>

{#if currentIndex > 0}
  <div class="prev" on:mousedown|stopPropagation on:click={$context.prev}>
    <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAB4AAABHCAYAAAAQsfedAAABgWlDQ1BzUkdCIElFQzYxOTY2LTIuMQAAKJF1kc8rRFEUxz8zgxGjUSjJYhI2ZsQosbEYMRQWY5TBZuaZH2p+vN4babJVtooSG78W/AVslbVSREpWFtbEhuk5b2ZqJHNu557P/d57TveeC9ZgUknpVX2QSme1gN/nmg8tuOwv1NBGCz0QVnR1enY8SEX7vMdixluPWavyuX+tfjmqK2CpFR5RVC0rPCE8tZZVTd4RblYS4WXhM2G3JhcUvjP1SJFfTY4X+dtkLRgYBWujsCv+iyO/WEloKWF5OZ2p5KpSuo/5Ekc0PTcrsUO8HZ0Afny4mGSMUQbpZ1jmQTx46ZUVFfL7CvkzZCRXkVklh8YKcRJkcYu6KtWjEmOiR2UkyZn9/9tXPTbgLVZ3+KD62TDeu8C+Dfktw/g6Moz8Mdie4DJdzs8cwtCH6FtlrfMAnBtwflXWIrtwsQmtj2pYCxckm7g1FoO3U2gIQdMN1C0We1ba5+QBguvyVdewtw/dct659ANjO2fkAC8C5AAAAAlwSFlzAAAuIwAALiMBeKU/dgAAA8dJREFUaIHd2kuoV1UUx/HPVUto4KRByepBKFFWUJjmoySIsgahYmWSPcCKHoMosiKiN0UZSEQUJUElqWRRRBSBNbGHlE1MB6FB4QKlhz0sTb3eBmdrf/Xe7v/e/zn/qDXa55y91/e/zvmdvdfa59+ji5aZY/EuvhnZRehovIdJ6B3RJWgPnsUU7MR1XQHjFiws7YUR8WXjxMw8PzP3ZmZfZj6x/3yjEWfmiXgdI/E+7t1/radB6FH4GGdiEyZHxPb91xuJuIjppQLdgVmt0MbAuAvzSntBRGxsiPO3ZeYlmbmviOn+gfrVGnFmnozlKu28iUcH6lubuDJzDNbiFHyFqRGxY6D+tUScmSOwrEC3Y/Y/QWsD4yFcin24IiI21+R3YMvMuUVIfZl5R7vjOoo4M8/Ay+VwGZa0O3bY4srMo/E5TsIXmBERO9sdP6yIM3MUVhboNswZCnTYYCzGBdiDuRGxZZh+2rfMvKZFTDc2DizQyZm5q0Cf68RX27c6M49VTYOjsQa3dQJuS9UlUfsQ07AFZ0fEtk7Ag0Zc1tZnCnSXajrsCNoWGDfhhtK+PiLWdQod1DJzRmbuKWJaXKfvASPOzBOwCqPwAe6pE9yvuEqitgZnYTMmHZozdWqHRVzEtLRA+03UGgHjTswv7asjYkPd0MMsM2dmZm8R04NNsg5EnJnjsaKcewsPNwnuKdAx+AynYoMqUfutSfCIkqi9WqA/q2amRqFU7+gnOAd9mBcRm5qGQk9m9pX21ogY2w0olZDWlvYxmTmzm+BpeFsltBVF3Y1bq6o/xQRsxJTGVQ0R8StmqVQ9Aa8UtTcLLvBNuFJVhszGgCVmI5aZi1qyyDlNcfq7nU+palyqW35aE+B21+PJEfFTneB+BRQRf6ie8/cYh+WlbGkWXODf4TLsxUV4vE7woJaZN7eI7aq6/Lbzrj6PF0t7aWZOrAPcbiVxJD7SzUoCImI35iJxHFaVH9MsuMC3Yg7+xLl4uhPwkO1fqY9b4EsKeHdmTh+Oj+GuQIuwGkfgjcw8fqgO6tr1WYfzGt/1gYj4UbWG/46JeKGUP82CC3w9ri2HC3B7J/6GbJn5SBFbb2Ze2M6YutKbB/BO8bcyM8cNNuC/vV/NQQnjLzjdIAljrZlkRHytShj7VNPrfXX6H9Qy8+6WaXVWf32ayp2fVNXasCwzJxza4f/1pY2DEsYfMB6vZeaB79WNlikR8S0uRy8uxmNN8g6zzLy1RWzzafAZHwLuUSWMC1UbsdO7Ai7w0aqEcSrWdw1c4Af+FfEXU/DP+D+3QVgAAAAASUVORK5CYII=" alt="">
  </div>
{/if}
{#if currentIndex < $context.numScreens - 1}
  <div class="next" on:mousedown|stopPropagation on:click={$context.next}><img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAB4AAABHCAYAAAAQsfedAAABgWlDQ1BzUkdCIElFQzYxOTY2LTIuMQAAKJF1kc8rRFEUxz8zgxGjUSjJYhI2ZsQosbEYMRQWY5TBZuaZH2p+vN4babJVtooSG78W/AVslbVSREpWFtbEhuk5b2ZqJHNu557P/d57TveeC9ZgUknpVX2QSme1gN/nmg8tuOwv1NBGCz0QVnR1enY8SEX7vMdixluPWavyuX+tfjmqK2CpFR5RVC0rPCE8tZZVTd4RblYS4WXhM2G3JhcUvjP1SJFfTY4X+dtkLRgYBWujsCv+iyO/WEloKWF5OZ2p5KpSuo/5Ekc0PTcrsUO8HZ0Afny4mGSMUQbpZ1jmQTx46ZUVFfL7CvkzZCRXkVklh8YKcRJkcYu6KtWjEmOiR2UkyZn9/9tXPTbgLVZ3+KD62TDeu8C+Dfktw/g6Moz8Mdie4DJdzs8cwtCH6FtlrfMAnBtwflXWIrtwsQmtj2pYCxckm7g1FoO3U2gIQdMN1C0We1ba5+QBguvyVdewtw/dct659ANjO2fkAC8C5AAAAAlwSFlzAAAuIwAALiMBeKU/dgAAA9tJREFUaIHNmVuIVlUUx39+DZoPQQldYFlBDUlaD6WC4kgg5QQRM84EmjcE08nIHtKiHsLMB8PKhwqKTCg1msBhqpeIwpeUBq8vmUQXsPhTmqQ0WqPWfD3spZ25fbez96n/09nfOWv/WHuvb5219hknaTdwC/CAmf1MQSoBU4C7gB5JE4oErwAGgNnA65LGFQI2s0PASh8/AqwpAnxZkrZIKku6KOme1LxS5vpZ4FOgCdgt6eaU4CH7KekaYD/QDBwBWszsjxTgrMeY2WmgHThLiPTtqYKtNPwHMzsKLPXhIuCpFOAxJWmDB9ugpPtjzz/C44w2Ab2EOOiWdFtMcMX9k3QV8CUwDTgGzDKz32OAK3mMmfUDbcBp4HZgl6SKNlHADv8eWAgMAg8Cz8cA1yxJ6zzYypI68s5Xz7JtBXb59Q5Jd+YB15UcJE0EvgCmAz8AM83st0bAdQWKmf0JLABOEoqHDyQ1JQc7/CegE7gI3AtsaQTcsCR1ZYJtedHwNx08IGlmPbZ5k8ETwF5gAtAr6YZaDXO/8iRdDxwEJgP7gHlmdqGaXe70Z2YnCJE+AMwBXqvFLkreNbODwCofrpb0aIx5a5aklzMF49xKz0bxOKNngM8IBWOPpJvGejB6PSVpEnCAkNkOA3NHKxhje4zn7jbgHHA3sG20gjE62OFfAct8uBhYl4IzpiRt9GD7W1Jr9l4SjzPaCHzknG5JzZduJO8MvWDsA6YCXxMKxv5CWlL39ABwNWEFOgoBO7wV+ISwyn2FgR1+ArgO0gdXFtoKXOvDvkLAvsfdhGX+EJhTdFQfBWabWX9Sj73d2enQM0C7t0XJ93gDIW8PAgvN7LvEPJDUkalC1w+/n8RjSXcAO3z4HvDK8GeKeB+3eAcyRFE99nam26G/AgtGg0YHAy8C9wF/AZ1m9mPk+UdK0tJMMFWtMqPssaQZ/NtRvGVmXdVsci+1dxK9Dt0HrK3FLpfHksYDewgdhIAZZvZLLbZ5PX7VoecJ6bAmaC6wpC7g0l6u8jYmrSS1eJtSlrS1kTnq9ljSjUAPoU35HHi6EXAjpz57CR1CMac+3oZsc+g5oK1RaF1g4ElgiV8v9zYlrSTN9zakLOmFGHNW9VjSrYQ3Tgn4mEiHqP+/82ov1N516BlCMEWBVgQDzxFOcwaBh83s21jQMSWpPfNubShBVNMIjyVNI9TCAO8DL6UA//df2iRdQfjbNAOnCIVaEugQMLAZmE8o1B4ys+OpoJclaXEmmB5LDgRKkqYD2338NvBGIWDgHeBKQoZ63MzKRYCbgG8I3xc6zex8EVCAfwDwycIiz6VLTwAAAABJRU5ErkJggg==
" alt=""></div>
{/if}
{#if $context.numScreens > 1}
  <div class="dots">
    {#each Array($context.numScreens) as _, index}
      <div class="dot" on:click={() => $context.jump(index)}></div>
    {/each}
    <div class="active dot" style="left: {currentIndex * 26}px"></div>
  </div>
{/if}

<style>
.next, .prev {
  position: absolute;
  top: 50%;
  cursor: pointer;
  background-color: rgba(40,41,48, 0.8);
  padding: 8px 12px;
  transform: translateY(-50%);
  user-select: none;
}
.dots {
  position: absolute;
  bottom: 12px;
  left: 50%;
  white-space: nowrap;
  transform: translateX(-50%);
}
.dot {
  border: 1px solid #e5e5e5af;
  width: 14px;
  height: 14px;
  margin: 6px;
  cursor: pointer;
  border-radius: 12px;
  box-sizing: border-box;
  display: inline-block;
  background-color: rgba(40,41,48, 0.8);
}
.dot.active {
  transition: left 0.3s;
  position: absolute;
  border: none;
  background-color: #e5e5e5;
}
.next img, .prev img {
  width: 15px;
}
.next {
  right: 0%;
}
.prev {
  left: 0%;
}

</style>