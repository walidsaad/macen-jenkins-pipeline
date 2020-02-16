FROM tomcat:8.0-alpine
ADD /home/stagiaire/.m2/repository/com/mycompany/app/training-webapp/1.0-SNAPSHOT/training-webapp-1.0-SNAPSHOT.war /usr/local/tomcat/webapps/
EXPOSE 8080
CMD ["catalina.sh", "run"]
