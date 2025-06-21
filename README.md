// executor.js
// Executor de funções JavaScript dinâmico e seguro

/**
 * Executa uma função JavaScript passada como string.
 * @param {string} funcStr - String com o código da função.
 * @param {Array} args - Argumentos para passar à função.
 * @returns {any} Retorno da função.
 */
function executar(funcStr, args = []) {
  let func;
  try {
    // Cria uma função anonima a partir da string
    func = new Function('args', `"use strict"; return (${funcStr})(...args)`);
  } catch (err) {
    throw new Error('Erro ao compilar a função: ' + err.message);
  }

  try {
    return func(args);
  } catch (err) {
    throw new Error('Erro ao executar a função: ' + err.message);
  }
}

// Exemplo de uso:
const resultado = executar(
  'function(a, b) { return a * b + 10; }',
  [5, 3]
);
console.log(resultado); // 25

module.exports = { executar };
