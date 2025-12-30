cicd with docker


- name: Deploy to EC2
  uses: appleboy/ssh-action@v1
  with:
    host: ${{ secrets.EC2_HOST }}
    username: ubuntu
    key: ${{ secrets.EC2_KEY }}
    script: |
      docker pull your-username/your-image:latest
      docker stop flask-app || true
      docker rm flask-app || true
      docker run -d -p 80:5000 --name flask-app your-username/your-image:latest


## How it Works

git push
  ↓
Tests run
  ↓
Docker image built
  ↓
Image pushed to Docker Hub
  ↓
EC2 pulls latest image
  ↓
Old container replaced
  ↓
App live 🚀
