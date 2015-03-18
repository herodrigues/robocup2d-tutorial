```cpp
/*!
  \brief Calcula a taxa do chute
  \param dist Distança do jogador para a bola
  \param dir_diff Diferença entre o ângulo do jogador e da bola
  \param kprate Taxa de força do chute do jogador
  \param bsize Raio da bola
  \param psize Raio do jogador
  \param kmargin Margem da área chutável do jogador 
  \return Taxa do efeito da força de chute

  Pode ser útil redefenir esse algoritmo no módulo do chute
*/
inline double kick_rate( const double & dist,
           const double & dir_diff,
           const double & kprate,
           const double & bsize,
           const double & psize,
           const double & kmargin )
```