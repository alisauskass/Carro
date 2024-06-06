

//motor_A
int IN1 = 10 ;
int IN2 = 11 ;
int ENA = 5 ;
int ENB = 6 ;


//motor_B
int IN3 = 13 ;
int IN4 = 12 ;

const int VELOCIDADE = 100;
const int DURACAO_ANDAR = 400; //
const int DURACAO_PARAR = 1000;

int speed = VELOCIDADE;

void setup(){
  pinMode(6, OUTPUT);
  pinMode(5, OUTPUT);
  pinMode(IN1,OUTPUT);
  pinMode(IN2,OUTPUT);
  pinMode(IN3,OUTPUT);
  pinMode(IN4,OUTPUT);
  Serial.begin(9600); // inicializa comunicação serial
}

void moveForward(int speed) {
  digitalWrite(IN1, HIGH);
  digitalWrite(IN2, LOW);
  digitalWrite(IN3, LOW);
  digitalWrite(IN4, HIGH);
  analogWrite(ENB, speed);
  analogWrite(ENA, speed);
}

void moveBackward(int speed) {
  digitalWrite(IN1, LOW);
  digitalWrite(IN2, HIGH);
  digitalWrite(IN3, HIGH);
  digitalWrite(IN4, LOW);
  analogWrite(ENB, speed);
  analogWrite(ENA, speed);
}

void stopMotor() {
  digitalWrite(IN1, LOW);
  digitalWrite(IN2, LOW);
  digitalWrite(IN3, LOW);
  digitalWrite(IN4, LOW);
  analogWrite(ENB, 0);
  analogWrite(ENA, 0);
}

void loop(){
  if (Serial.available() > 0) { // verifica se há input disponível
    char c = Serial.read(); // lê o caractere input
    switch (c) {
      case 'w':
      case 'W':
        moveForward(VELOCIDADE);
        break;
      case 'a':
      case 'A':
        moveBackward(VELOCIDADE);
        break;
      default:
        stopMotor();
        break;
    }
  }
  delay(50); // aguarda um pouco antes de ler novamente
}
