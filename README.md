# Projeto-React-

import { useEffect, useState } from "react";
import "./App.css";

function App() {
  const [usuario, setUsuario] = useState(null);
  const [carregando, setCarregando] = useState(true);
  const [erro, setErro] = useState("");

  useEffect(() => {
    fetch("https://api.github.com/users/alicepereirajsd-dotcom")
      .then((resposta) => {
        if (!resposta.ok) {
          throw new Error("Não foi possível carregar o perfil.");
        }

        return resposta.json();
      })
      .then((dados) => {
        setUsuario(dados);
        setCarregando(false);
      })
      .catch((erro) => {
        setErro(erro.message);
        setCarregando(false);
      });
  }, []);

  if (carregando) {
    return (
      <div className="mensagem">
        Carregando perfil...
      </div>
    );
  }

  if (erro) {
    return (
      <div className="mensagem erro">
        {erro}
      </div>
    );
  }

  return (
    <main className="pagina">

      <section className="container">

        {/* LADO ESQUERDO */}
        <div className="lado-esquerdo">

          <div className="topo">
            <span className="icone-codigo">
              &lt;/&gt;
            </span>

            <span>
              Desenvolvedora em formação
            </span>
          </div>

          <p className="ola">
            Olá! 👋
          </p>

          <h1>
            Alice <span>Ferreira</span>
          </h1>

          <p className="username">
            @{usuario.login}
          </p>

          <div className="linha"></div>

          <div className="descricao">
            <p>
              Estudante de Desenvolvimento de Sistemas.
            </p>

            <p>
              Busco aprimorar ainda mais os meus conhecimentos nessa nova etapa. 💜
            </p>
          </div>

          {/* TECNOLOGIAS */}
          <div className="tecnologias">

            <span className="tecnologia html">
              HTML
            </span>

            <span className="tecnologia css">
              CSS
            </span>

            <span className="tecnologia javascript">
              JavaScript
            </span>

            

            

            <span className="tecnologia git">
              Git & GitHub
            </span>

          </div>

          {/* FRASE */}
          <div className="frase">

            <span className="aspas">
              “
            </span>

            <p>
              Transformando ideias em código,
              <br />
              e código em aprendizado.
            </p>

          </div>

        </div>


        {/* LADO DIREITO */}
        <div className="lado-direito">

          {/* FOTO */}
          <div className="foto-container">

            <div className="orbita"></div>

            <div className="foto">

              <img
                src={usuario.avatar_url}
                alt={`Foto de ${usuario.name}`}
              />

            </div>

            <div className="bolinha"></div>

          </div>


          {/* ESTATÍSTICAS */}
          <div className="estatisticas">

            <div className="card-estatistica">

              <span className="icone">
                📁
              </span>

              <strong>
                {usuario.public_repos}
              </strong>

              <p>
                Repositórios
              </p>

            </div>


            <div className="card-estatistica">

              <span className="icone">
                ⭐
              </span>

              <strong>
                {usuario.followers}
              </strong>

              <p>
                Seguidores
              </p>

            </div>


            <div className="card-estatistica">

              <span className="icone">
                🔗
              </span>

              <strong>
                {usuario.following}
              </strong>

              <p>
                Seguindo
              </p>

            </div>

          </div>


          {/* BOTÃO */}
          <a
            href={usuario.html_url}
            target="_blank"
            rel="noreferrer"
            className="botao-github"
          >

            <span className="github">
              ●
            </span>

            Acessar meu GitHub

            <span className="externo">
              ↗
            </span>

          </a>


          <p className="texto-botao">
            Clique no botão para conhecer meus projetos
          </p>

        </div>

      </section>

    </main>
  );
}

export default App;
