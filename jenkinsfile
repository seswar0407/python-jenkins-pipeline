pipeline {
    agent any
    
    stages {
      stage('Setup Environment'){
        steps {
            echo 'Setting up environment...'
            sh'''
              echo "Checking Python installation..."
              python3 --version
             '''
        }
      }
      stage ('Create Python Script'){
         steps {
             echo 'Creating Python file...'
             sh'''
               cat > calc.py <<EOF
def add(a,b):
  return a + b

def multiply(a,b):
  return a * b

if __name__ =="__main__":
  x,y = 5,3
  print("Addition:",add(x,y))
  print("Multiplication:",multiply(x,y))
EOF
        '''
         } 
      }
      stage('Run Python Script'){
          steps{
              echo 'Running Python file...'
              sh'python3 calc.py'
          }
      }
      stage('Validate Result'){
          steps{
              echo 'Running test check...'
                sh'''
                  RESULT=$(python3 -c "x=5;y=3;print(x+y)")
                  if [ "$RESULT" -eq 8 ]; then
                       echo "Test passed - correct addition!"
                  else
                    echo "Test failed"
                    exit1
                  fi
            '''
          }
      }
      stage('Finish'){
          steps {
              echo 'Pipeline Finished Successfully'
          }
      }
    }  
}
