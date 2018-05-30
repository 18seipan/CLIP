# CLIP
//Code adapted and edited by Andy and Ethan 
//Arduino porting code + chart + list reset borrowed
//CLIP
//chart equivalent to an arraylist
#define students 15

const char *players[students]={
"Andy",
"Ethan", 
"Jess", 
"Justin", 
"Patrick", 
"Elliot", 
"Wade",
"Tristin", 
"Carl", 
"Kyle", 
"Steven", 
"Evan", 
"Zoe", 
"Noah",
"Sam",   
};

int choices[students];
int choicesMade;

void setup() 
{
  Serial.begin(9600);
  randomSeed(analogRead(A0));
  resetNames();
}

void loop() 
{
  int studentId = selectNameFromRemaining();
  if(studentId == -1)
  {
    Serial.println(F("Reseting Names..."));
    resetNames();
    delay(5000);
  }
  else
  {
    Serial.println(players[studentId]);
  }

  delay(1000);
}

int selectNameFromRemaining()
{
  if(choicesMade >= students)
  {
    return -1;
  }
  int selection = random(choicesMade, students);
  int temp = choices[choicesMade];
  choices[choicesMade] = choices[selection];
  choices[selection] = temp;
  return choices[choicesMade++]; 
}

bool resetList()
{
  for (int i = 0; i < students; i++)
  {
    choices[i] = i;
  }
  for (int i = 0; i < students; i++)
  {
    int index = random(i, students);
    int temp = choices[i];
    choices[i] = choices[index];
    choices[index] = temp;
  }
  choicesMade = 0;
}
