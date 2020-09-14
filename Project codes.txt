#include <GL/glut.h>    
#include <GL/gl.h>    
#include <GL/glu.h>   
//#include <unistd.h>     



/* ASCII KODLARI. */
#define ESCAPE 27
#define Space 32
#define DEL 127
#define BACKSPACE 8



GLfloat xt = 0.0, yt = 0.0, zt = 0.0, xw = 0.0;   /* x,y,z KOORDÝNATLARI */
GLfloat tx = 295, ty = 62;
GLfloat xs = 1.0, ys = 1.0, zs = 1.0;

int window;

static int spin = 0;
int key;


/* UCGENIN DONUS ACISI */
float donus = 0.0f;

/* DORTGENIN DONUS ACISI */
float dortgen = 0.0f;


void InitGL(int Width, int Height)
{
	// 
	glClearColor(0.0f, 0.0f, 0.0f, 0.0f);
	glClearDepth(1.0);                
	glDepthFunc(GL_LESS);               
	glEnable(GL_DEPTH_TEST);           
	glShadeModel(GL_SMOOTH);          
	glEnable(GL_LIGHTING);
	glEnable(GL_LIGHT0);


	glMatrixMode(GL_PROJECTION);
	glLoadIdentity();                // MATRISIN SIFIRLANMASI

	gluPerspective(45.0f, (GLfloat)Width / (GLfloat)Height, 0.1f, 100.0f);

	glMatrixMode(GL_MODELVIEW);
}


void ReSizeGLScene(int Width, int Height) //EKRAN BOYUTUNUN YENIDEN AYARLANMASI
{
	if (Height == 0)                
		Height = 1;

	glViewport(0, 0, Width, Height);        

	glMatrixMode(GL_PROJECTION);
	glLoadIdentity();

	gluPerspective(45.0f, (GLfloat)Width / (GLfloat)Height, 0.1f, 100.0f);
	glMatrixMode(GL_MODELVIEW);
	glViewport(0, 0, (GLsizei)Width, (GLsizei)Height);
	glMatrixMode(GL_PROJECTION);
	glLoadIdentity();
	gluPerspective(40.0, (GLfloat)Width / (GLfloat)Height, 1.0, 20.0);
	glMatrixMode(GL_MODELVIEW);
	glLoadIdentity();

}


float ballX = -0.5f;
float ballY = 0.0f;
float ballZ = 0.0f;

void drawBall(void) {
	glColor3f(1.0, 0.0, 0.0); //KIRMIZI RENK KODU
	glTranslatef(ballX, ballY, ballZ); 
	glutSolidSphere(0.2, 20, 20); 
	glTranslatef(ballX + 1.5, ballY, ballZ); 
	glutSolidSphere(0.22, 20, 20); 
}


/* ANA EKRAN */
void DrawGLScene()
{
	glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);        
	glLoadIdentity();                

	glTranslatef(donus, 0.1f, -4.0f);       

											
	glBegin(GL_POLYGON);
	

	glColor3f(1.0f, 1.0f, 1.0f);            // BEYAZ RENK KODU
	glVertex3f(-1.0f, 1.0f, 0.0f);        // ÜST TARAFIN ÞEKLÝ
	glVertex3f(0.3f, 1.0f, 0.0f);      // ARABA ÝÇÝN OLUÞTURULAN ÞEKÝL

	glVertex3f(1.0f, 1.0f, 0.0f);


	glColor3f(0.0f, 1.0f, 1.0f);            
	glVertex3f(1.0f, 0.0f, 0.0f);        
	glColor3f(1.0f, 0.0f, 1.0f);            
	glVertex3f(-1.5f, 0.0f, 0.1f);    

								 
	glEnd();                   
	drawBall();
	





	GLfloat position[] = { 0.0, 0.0, 1.5, 1.0 };
	//glClear (GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
	glPushMatrix();
	gluLookAt(0.0, 0.0, 5.0, 0.0, 0.0, 0.0, 0.0, 1.0, 0.0);
	glPushMatrix();
	glRotated((GLdouble)spin, 1.0, 1.0, 0.0);
	glLightfv(GL_LIGHT0, GL_POSITION, position);
	glTranslated(1.0, 1.0, 2.0);
	glDisable(GL_LIGHTING);
	glColor3f(1.0, 1.0, 1.0);
	glutWireCube(0.1);
	//glEnable (GL_LIGHTING);
	glPopMatrix();
	// glutSolidTorus (0.275, 0.85, 8, 15);
	glPopMatrix();
	glFlush();


	char key = 'a';
	GLint Xsize = 1000;
	GLint Ysize = 800;

	/* switch(key) {
	case 'a':
	Xsize += 0.2;
	glutPostRedisplay();
	break;
	if(key==a){
	donus += 0.005f;                    
	if (donus>2)
	donus = -2.0f;
	dortgen -= 15.0f;
	} 

	
	} */
	glutSwapBuffers();


}


void keyPressed(GLubyte key, GLint x, GLint y)
{
	GLfloat xt = 0.0, yt = 0.0, zt = 0.0, xw = 0.0;   /* x,y,z KOORDÝNATLARI */
	GLfloat tx = 295, ty = 62;
	GLfloat xs = 1.0, ys = 1.0, zs = 1.0;
	GLint Xsize = 1000;
	GLint Ysize = 800;
	float i, theta;
	
	switch (key) {

	case ESCAPE: {
		if (key == ESCAPE) {

			
			donus -= 0.010f;                   
			if (donus > 2)
				donus = 2.0f;
			dortgen += 20.0f;
		}
	case  Space: {
		if (key == Space)
			donus += 0.010f;                    
		if (donus > 2)
			donus = 2.0f;
		dortgen += 20.0f; }
	case DEL: {
		
		if(key==DEL)
		
			 {
						
			donus -= 20.100f;                   
			if (donus > 2)
				donus = 2.0f;
			dortgen += 5.000f;
			} 

	case BACKSPACE: {
	if (key==BACKSPACE)
		glutFullScreen();

	
	}
			
		
		
		

		

			


		/*	donus += 0.005f;                    
		if (donus>2)
		donus = -2.0f;
		dortgen -= 15.0f;

		*/




	}



				
				 break;


				 //case GLUT_KEY_RIGHT:
				 yt += 0.2;
				 glutPostRedisplay();
				 break;

				


	case 'u':                         
		yt += 0.2;
		glutPostRedisplay();
		break;

	case 'U':
		yt -= 0.2;                      
		glutPostRedisplay();
		break;

		/*case 'f':                          
		zt += 0.2;
		glutPostRedisplay();
		break;
		*/

	case 'F':
		zt -= 0.2;                     
		glutPostRedisplay();
		break;






	default:
		break;

		GLint Xsize = 1000;
		GLint Ysize = 800;
		

		
	
	}
	}
}


void mouse(int button, int state, int x, int y)
{
	switch (button) {
	case GLUT_LEFT_BUTTON:
		if (state == GLUT_DOWN) {
			spin = (spin + 40) % 360;
			DrawGLScene();
		}
		break;
	default:
		break;
	}
}



/*void keyboard(unsigned char key, int x, int y)
{
switch (key) {
case 27:
exit(0);
break;
}
}*/


int main(int argc, char **argv)
{
	glutInit(&argc, argv);

	glutInitDisplayMode(GLUT_RGBA | GLUT_DOUBLE | GLUT_ALPHA | GLUT_DEPTH);

	/* ÇERÇEVE BOYUTU */
	glutInitWindowSize(640, 480);

	/* EKRAN BAÞLANGIC KONUMU */
	glutInitWindowPosition(0, 0);

	
	window = glutCreateWindow("ARABA SÝMÜLASYONU");

	/* EKRANA ÇÝZDÝRME. */
	glutDisplayFunc(&DrawGLScene);

	/*TAM EKRAN YAPMA KOMUTU  */
	//glutFullScreen(); 

	/* SAHNEYÝ YENÝDEN ÇÝZME. */
	glutIdleFunc(&DrawGLScene);

	/* BOYUT DEÐÝÞTÝÐÝNDE SAHNEYÝ YENÝDEN ÞEKÝLLENDÝRME. */
	glutReshapeFunc(&ReSizeGLScene);

	/*KLAVYEDE TUÞLARA BASILDIGINDA . */
	glutKeyboardFunc(&keyPressed);
	

	glutMouseFunc(&mouse);

	/* EKRAN. */
	InitGL(640, 480);


	

	/* MAKÝNA DÖNGÜSÜ */
	glutMainLoop();

	return 1;
}