# T7-G31
## Istruzioni
La cartella per lanciare il codice è RemoteCCC_nozip.
Si utilizza maven per compilarlo , sotto windows si può lanciare il .cmd con il parametro help per leggere le possibilità.
Dualmente su Mac/unix il comando build.sh


## Attenzione
I path in config.java in src/main/java/RemoteCCC sono scritti per UNIX per utilizzare il codice su windows bisogna commentarli e decommentare gli altri.

## Per provarlo...

Lanciato build.sh run o build.cmd run dovrebbe partire sul terminale l'applicazione del server, a quel punto si può lanciare tramite postman una richiesta post con questo end-point compile-and-codecoverage in loopback : il body della richiesta deve essere fattoin Json come nell'esempio sottostante:
 
{"testingClassName": "TestLola.java","testingClassCode": "import org.junit.jupiter.api.Test;\nimport static org.junit.jupiter.api.Assertions.assertEquals;\nimport static org.junit.jupiter.api.Assertions.assertThrows;\n\npublic class TestLola {\n    @Test\n    public void testDivide() {\n        Lola cut = new Lola();\n\n        // Test division by non-zero number\n        int result = cut.divide(10, 2);\n        assertEquals(5, result);\n\n        // Test division by zero\n        assertThrows(ArithmeticException.class, () -> {\n            cut.divide(10, 0);\n        });\n    }\n}\n",
  "underTestClassName": "Lola.java",
  "underTestClassCode": "public class Lola {\n    public int divide(int a, int b) {\n        if (b == 0) {\n            throw new ArithmeticException(\"Cannot divide by zero\");\n        }\n        return a / b;\n    }\n}\n"
}



## RemoteCCC
Questa è una versione del codice dove però il ritorno della copertura è dato in formato zip passando tutti ifile necessari per aprire index.html dato dalla copertura di jacoco, mentre in quella no_zip è ritornato esclusivamente il file xml.
