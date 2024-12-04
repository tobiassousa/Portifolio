# Beta
1° Semestre - 01/2022

Parceiro: Professor Fatec - Fabiano Sabha

<div align="center">
<img src="https://user-images.githubusercontent.com/102003274/160285282-b3d220d2-bf73-4aba-9c86-74a6a4b640b0.png" width="200px" />
</div>

## 💻 Nossa proposta
A BETA é uma assistente criada por nós com intenção de oferecer suporte a alunos, em seu tempo de estudo, foco e algumas atividades para auxiliar melhor a compreensão do ensinamento.
Possuindo varias funcionalidade como:
 Pesquisa, Pomodoro, Calendário, Toque, Gravador de voz, Livro, Clima, Calculadora ou lembrete.

Para ativar suas funcionalidades é necessario apenas falar a nomenclatura da função. 

## Projeto:
https://github.com/tobiassousa/Beta




## Contribuições Individuais
<details>
  <summary><b>Implementação da funcionalidade de pomodoro.</b></summary>
  <br>
  <p>O código apresentado é parte do desenvolvimento da assistente virtual BETA, que tem como objetivo realizar a funcionalidade do pomodoro, o qual a iniciar começa a contar durante 25 mintuos, após isso realiza a pausa de 5 minutos e volta a contar os 25 minutos:
  </p>
  
```python
elif 'pomodoro' in comando:

            t_now = dt.datetime.now()  # data e hora atual;

            t_pom = 25 * 60  # tempo de duração do fluxo pomodoro 25m;

            t_delta = dt.timedelta(0, t_pom)  # diferença de tempo;

            t_fut = t_now + t_delta  # hora que o pomodoro termina e começa a pausa;

            delta_sec = 5 * 60  # definição de intervalo;

            t_fin = t_now + dt.timedelta(0, t_pom + delta_sec)  # hora que a pausa termina;

            pomodoro = pyttsx3.init()

            pomodoro.say("Pomodóro iniciado " "\n\nAgora é " + t_now.strftime(

                "%H:%M") + " hrs. \n\nTemporizador definido por 25 minutos")

            pomodoro.runAndWait()

            total_pomodoros = 0

            breaks = 0

            # Looping simples dividido em três seções: Hora pomodoro, intervalo e fim do código;

            while True:

                if dt.datetime.now() < t_fut:

                    print('Pomodóro')

                elif t_fut <= dt.datetime.now():

                    if total_pomodoros in range(3, 100, 5):

                        for i in range(1):
                            winsound.Beep((i + 400), 500)  # Primeiro número é referente ao volume do bip.

                        print('Hora do intervalo! Você tem 25 minutos de descanso.')

                        breaks += 1

                        audio = sr.Recognizer()

                        pomodoro = pyttsx3.init()

                        pomodoro.say('Hora do intervalo!')

                        pomodoro.runAndWait()

                        time.sleep(
                            5)  # Por conta do delay da fala subtrair do tempo de pausa um tempo,então o que era pra ser 25 min ficou 21 min

                        print("Foi")

                    if breaks == 0:

                        for i in range(2):
                            winsound.Beep((i + 400), 700)  # Primeiro número é referente ao volume do bip.

                        print('Hora do intervalo!')

                        breaks += 1

                        audio = sr.Recognizer()

                        pomodoro = pyttsx3.init()

                        pomodoro.say('Hora do intervalo! Você tem 5 minutos de descanso.')

                        pomodoro.runAndWait()

                        time.sleep(
                            5)  # Por conta do delay da fala subtrair do tempo de pausa um tempo,então o que era pra ser 5 min ficou o tempo determinado como 1260 dividido por 5, pra ficar um descanso proporcional.

                    else:

                        print('Fim')

                        breaks = 0

                        for i in range(1):
                            winsound.Beep((i + 400), 700)  # Primeiro número é referente ao volume do bip.

                            audio = sr.Recognizer()

                            pomodoro = pyttsx3.init()

                            pomodoro.say('O intervalo acabou, deseja iniciar um novo pomodóro?')

                            pomodoro.runAndWait()

                        usr_ans = messagebox.askyesno("Fim da primeira sequência do pomodóro",

                                                      "Deseja iniciar outra sequência de pomodóro?")

                        total_pomodoros += 1

                        print(total_pomodoros)

                        if usr_ans == True:

                            t_now = dt.datetime.now()

                            t_fut = t_now + dt.timedelta(0, t_pom)

                            t_fin = t_now + dt.timedelta(0, t_pom + delta_sec)


                        elif usr_ans == False:

                            msg = messagebox.showinfo("Fim do pomodóro",

                                                      "\nVocê completou " + str(total_pomodoros) + " pomodóro(s) hoje!")

                            break

                    print("sleeping")

                    time.sleep(1)

                    t_now = dt.datetime.now()

                    timenow = t_now.strftime("%H:%M")
```
 
 <p>No código fornecido, é realizado o reconhecido a chamada da funcionalidade e realiza o inicio da contagem de tempo, após esse tempo ele mostra uma tela avisando o fim do tempo por uma janela do tkinter, quando ocorre a confirmação começa a contagem do intervalo, e apresenta novamente o aviso de seu fim e inicia novamente o ciclo.</p>
  <br>
</details>
<details>
  <summary><b>Gravação de Áudio</b></summary>
  <br>
  <p>Neste trecho de código, quando o usuário fala "beta", a assistente inicia a gravação de áudio por 5 segundos. Abaixo está uma explicação detalhada do que acontece:</p>
  
```python
import sounddevice as sd
from scipy.io.wavfile import write
import os

freq = 44100  # Frequência do áudio: 4999 - 64000
seconds = 5  # Duração da gravação

gravacao = sd.rec(int(seconds * freq), samplerate=freq, channels=2)
print("Começando: Fale agora!!")
sd.wait()  # Comando de inicialização da gravação.
print("Fim da gravação!")
write('output.wav', freq, gravacao)  # Salva a gravação como arquivo WAV.
os.startfile("output.wav")           # Abre gravação.
```  
  <p>O código utiliza a biblioteca `sounddevice` para capturar áudio do microfone e `scipy.io.wavfile` para salvar a gravação como arquivo WAV.</p>
  <p>As variáveis `freq` e `seconds` definem a frequência de amostragem do áudio e a duração da gravação, respectivamente. No caso, a gravação dura 5 segundos com uma frequência de 44100 Hz.</p>
  <p>O comando `sd.rec()` inicia a gravação do áudio com base nas configurações especificadas.</p>
  <p>Os comandos `print()` exibem mensagens indicando o início e o fim da gravação.</p>
  <p>O comando `sd.wait()` é responsável por aguardar o término da gravação.</p>
  <p>Após a gravação, o áudio é salvo como um arquivo WAV utilizando o comando `write()`. O arquivo é nomeado como "output.wav".</p>
  <p>Finalmente, o comando `os.startfile()` é usado para abrir o arquivo de áudio recém-gravado, reproduzindo-o no sistema padrão do usuário.</p>
  <br>
</details>




## Tecnologias Utilizadas

Python: Linguagem de programação principal utilizada para desenvolver a lógica da assistente virtual e suas funcionalidades.

Tkinter: Biblioteca gráfica do Python utilizada para criar a interface gráfica da aplicação.






## Lições Aprendidas

<p align="justify"></p>
<h3>Hard Skills</h3>
<details>
  <summary><b>Clique para ver a lista de hard skills</b></summary>
<p1>Desenvolvimento de Software: Fortaleci minhas habilidades em Python criando a função de pomodoro da qual necessitei aprender a realizar a logica de programação, e também a verificar a aprendizagem da maquina a reconhecer a chamativa para a funcionalidade.</p1>

<p1>Desenvolvimento de Interface: Utilizei Tkinter para criar interfaces gráficas intuitivas, das quais realizam avisos na tela quando começa e acaba o tempo do pomodoro.</p1>

</details>
<h3>Soft Skills</h3>
<details>
  <summary><b>Clique para ver a lista de soft skills</b></summary>
<p1>Trabalho em Equipe: A colaboração com o time é fundamental para conseguir realizar uma entrega completa. Sendo assim foi utilizado o whatsapp para trocas de mensagens diarias e realizado encontros durantes as aulas.</p1>

<p1>Gestão do Tempo: Realizei o planejamento dos dias de até a entrega e o tempo gasto da atividade para entregar a tempo.</p1>

</details>


## Meus Projetos
## Semestres

- [Semestre 2 - Pro4Tech](./Semestre02/Semestre02.md)
- [Semestre 3 - Dom Rock](./Semestre03/Semestre03.md)
- [Semestre 4 - Jaia](./Semestre04/Semestre04.md)
- [Semestre 5 - Tecsus](./Semestre05/Semestre05.md)
- [Semestre 6 - SPC Grafeno](./Semestre06/Semestre06.md)
