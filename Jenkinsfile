pipeline{
    agent any
    stages{
        stage("Test"){
            steps{
                sh '''
                       echo "Hello World"
                   '''
            }
        }
        stage("Build"){
            steps{
                sh '''
                      ## Get the project
                       
                       sudo apt update

                       sudo docker build -t monyslim/pixer:latest .

                       sudo docker run -d -p 801:80 monyslim/pixer:latest
                   
                   
                   
                   '''
            }
        }
    }
}
