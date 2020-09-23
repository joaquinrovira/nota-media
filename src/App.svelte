<script>
  let n_test = 40;
  let vp_t_mal = 0.025;
  let vp_t_acertada = 0.1;

  let n_desarrollo = 2;
  let vp_d_max = 0.5;
  let vp_d_expected = 0.7;

  let exp = "";
  let result5 = "";
  let result8 = "";

  function calc(...args) {
    for (const e of args) {
      if (e === "" || isNaN(e)) return;
    }

    const max_nota = n_test * vp_t_acertada + n_desarrollo * vp_d_max;
    const val5 = max_nota * 0.5;
    const val8 = max_nota * 0.8;
    const exp_des = n_desarrollo * vp_d_max * vp_d_expected;

    exp = exp_des;
    result5 = Math.ceil((val5 - exp_des) / vp_t_acertada);
    result8 = Math.ceil((val8 - exp_des) / vp_t_acertada);
  }

  $: calc(
    n_test,
    vp_t_mal,
    vp_t_acertada,
    n_desarrollo,
    vp_d_max,
    vp_d_expected
  );
</script>

<style>
</style>

<div container flex-col>
  <!-- Test Section -->
  <div flex-col border style="background-color: thistle;">
    <!-- 1st row -->
    <div flex>
      <div flex ccenter>
        <h2>Test</h2>
      </div>
      <div flex-col ccenter>
        <span>Número de preguntas:</span>
        <input bind:value={n_test} />
      </div>
    </div>
    <!-- 2nd row -->
    <div flex>
      <div flex-col ccenter>
        <span>Puntuación por pregunta mal:</span>
        <input bind:value={vp_t_mal} />
      </div>
      <div flex-col ccenter>
        <span>Puntuación por pregunta acertada:</span>
        <input bind:value={vp_t_acertada} />
      </div>
    </div>
  </div>
  <!-- Desarrollo Section -->
  <div flex-col border style="background-color: khaki;">
    <!-- 1st row -->
    <div flex>
      <div flex ccenter>
        <h2>Desarrollo</h2>
      </div>
      <div flex-col ccenter>
        <span>Número de preguntas:</span>
        <input bind:value={n_desarrollo} />
      </div>
    </div>
    <!-- 2nd row -->
    <div flex>
      <div flex-col ccenter>
        <span>Puntuación por pregunta:</span>
        <input bind:value={vp_d_max} />
      </div>
      <div flex-col ccenter>
        <span>Puntuación esperada (sobre 1):</span>
        <input bind:value={vp_d_expected} />
      </div>
    </div>
  </div>
  <!-- Resultados Section -->
  <div flex-col border style="background-color: lightcyan;">
    <!-- 1st row -->
    <div flex>
      <div flex ccenter>
        <h2>Resultado</h2>
      </div>
    </div>
    <!-- 2nd row -->
    <div>
      Con una puntuación esperada en el apartado de desarrollo de <b>{exp}</b>.
    </div>
    <h2>Para sacar un 5:</h2>
    <div>
      Tendrías que acertar un mínimo de <b>{result5} preguntas</b> test sin fallar.
    </div>
    <h2>Para sacar un 8:</h2>
    <div>
      Tendrías que acertar un mínimo de <b>{result8} preguntas</b> test sin fallar.
    </div>
  </div>
</div>
