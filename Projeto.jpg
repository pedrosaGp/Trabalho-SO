#include <stdio.h>
#include <conio.h>
#include <string.h>
#include <stdlib.h>
#include <ctype.h>
struct documento
{
    char numero[5];
    char ano[5];
    char tipo_cod[5];
    char resp_cod[5];
    char data[10];
    char assunto[100];
    char inativo[2];
    char status;
} doc;
FILE *fdoc;
/*prototipo das funcoes*/
void incluir (void);
void consultar(void);
void excluir(void);
void alterar(void);
void abrir(void);
void listar(void);

int main(void)
{
    char opcao[2], op;
    do
    {
        do
        {
            system("cls");
            printf("\n\n\n\n\n\n\n");
            printf("\t####################################\n");
            printf("\t# #\n");
            printf("\t# Programa de Controle de Documentos #\n");
            printf("\t# #\n");
            printf("\t###################################\n\n");
            printf("\n Digite uma das opcoes\n\n");
            printf("\n I - Incluir");
            printf("\n A - Alterar");
            printf("\n E - Excluir");
            printf("\n C - Consultar");
            printf("\n L - Listar");
            printf("\n S - Sair");
            printf("\n\n\n Opcao:");
            gets(opcao);
            op=tolower(*opcao);
        }
        while(!strchr("iaeclsh",op));
        switch(op) /*D*/
        {
        case 'i' :
            incluir();
            break;
        case 'a' :
            alterar();
            break;
        case 'e' :
            excluir();
            break;
        case 'c' :
            consultar();
            break;
        case 'l' :
            listar();
            break;
        case 's' :
            exit(0);
        }
    }
    while(1);
}
/*Funcoes*/
void abrir(char tipo[3])
{
    if((fdoc=fopen("C:/documento.txt", tipo))==NULL)
    {
        printf("\nO arquivo nao pode ser aberto!! \n");
        getch();
        exit(1);
    }
}
void incluir(void)
{
    abrir("ab+");
    fseek(fdoc,0L, SEEK_END);

    do
    {
        printf("\n Digite o numero ou <FIM> para sair:\n\n");
        gets(doc.numero);

        if ((strcmp(doc.numero,"fim")!=0)&&(strcmp(doc.numero,"FIM")!=0))
        {
            printf("\n Ano(1990):");
            gets(doc.ano);
            printf("\n Tipo(codigo):");
            gets(doc.tipo_cod);
            printf("\n Responsavel(codigo):");
            gets(doc.resp_cod);
            printf("\n Data (31/12/1990):");
            gets(doc.data);
            printf("\n Assunto:");
            gets(doc.assunto);
            printf("\n Inativo (0=Ativo e 1=Inativo):");
            gets(doc.inativo);
            doc.status='1';
            if(fwrite(&doc, sizeof(struct documento), 1, fdoc) != 1)
            {
                printf("\n Erro de gravacao!");
                getch();
            }
            else
            {
                printf("\n Gravacao feita com sucesso!\n\n");
            }
        }
    }
    while((strcmp(doc.numero,"fim")!=0)&&(strcmp(doc.numero,"FIM")!=0));
    fclose(fdoc);
}
int busca (void)
{
    int achou=-1,posicao=0;
    char numerop[5];
    abrir("rb");
    printf("\nDigite o numero para consultar:");
    gets(numerop);
    rewind(fdoc);
    while((!feof(fdoc))&&(achou==-1))
    {
        fread(&doc, sizeof(struct documento), 1, fdoc);
        if (!feof(fdoc))
        {
            if (strcmp(numerop, doc.numero)==0)
            {
                if (doc.status=='0')
                {
                    posicao=-2;
                }
                achou=1;
            }
            else
            {
                posicao++;
            }
        }
        else
        {
            posicao=-1;
        }
    }
    if (achou==-1)
    {
        posicao=-1;
    }
    fclose(fdoc);
    return(posicao);
}
void consultar(void)
{
    int pos;
    pos=busca();
    if(pos==-1)
    {
        printf("\nNumero inexistente!");
        getch();
    }
    else if(pos==-2)
    {
        printf("\nNumero inexistente no arquivo!");
        getch();
    }
    else
    {
        abrir("rb+");
        fseek(fdoc,pos*sizeof(struct documento),SEEK_SET);
        fread(&doc, sizeof(struct documento), 1, fdoc);
        printf("\n\n----------------------------------------");
        printf("\nNumero:%s",doc.numero);
        printf("\nAno:%s",doc.ano);
        printf("\nTipo:%s",doc.tipo_cod);
        printf("\nResponsavel:%s",doc.resp_cod);
        printf("\nData:%s",doc.data);
        printf("\nAssunto:",doc.assunto);
        printf("\nInativo:",doc.inativo);
        getch();
    }
    fclose(fdoc);
}
void alterar(void)
{
    int pos;
    pos=busca();
    if (pos==-1)
    {
        printf("\nNumero inexistente no arquivo");
        getch();
    }
    else if(pos==-2)
    {
        printf("\nNumero inexistente no arquivo!");
        getch();
    }
    else
    {
        abrir("rb+");
        fseek(fdoc,pos*sizeof(struct documento),SEEK_CUR);
        fread(&doc, sizeof(struct documento), 1, fdoc);
        printf("\nDeseja alterar o seguinte registro?");
        printf("\nNumero:%s",doc.numero);
        printf("\nAno:%s",doc.ano);
        printf("\nTipo:%s",doc.tipo_cod);
        printf("\nResponsavel:%s",doc.resp_cod);
        printf("\nData:%s",doc.data);
        printf("\nAssunto:%s",doc.assunto);
        printf("\nInativo:%s",doc.inativo);
        getch();
        printf("\nDigite as informacoes corretas:");
        printf("\nNumero:");
        gets(doc.numero);
        printf("\nAno:");
        gets(doc.ano);
        printf("\nTipo:");
        gets(doc.tipo_cod);
        printf("\nResponsavel:");
        gets(doc.resp_cod);
        printf("\nData:");
        gets(doc.data);
        printf("\nAssunto:");
        gets(doc.assunto);
        printf("\nInativo:");
        gets(doc.inativo);
        doc.status='1';
        fseek(fdoc,pos*sizeof(struct documento),SEEK_SET);
        if(fwrite(&doc, sizeof(struct documento),1, fdoc)!=1)
        {
            printf("\nErro na gravacao!");
        }
        else
        {
            printf("\nAlteracao feita com sucesso!");
            getch();
        }
    }
    fclose(fdoc);
}
void listar(void)
{
    int cont=0;

    abrir("rb");
    fseek(fdoc, 0L, SEEK_SET);
    fread(&doc, sizeof(struct documento),1, fdoc);
    do
    {
        if (doc.status!='0')
        {
            printf("\n---------------------------------------");
            printf("\nNumero:%s",doc.numero);
            printf("\nAno:%s",doc.ano);
            printf("\nTipo:%s",doc.tipo_cod);
            printf("\nResponsavel:%s",doc.resp_cod);
            printf("\nData:%s",doc.data);
            printf("\nAssunto:%s",doc.assunto);
            printf("\nInativo:%s",doc.inativo);
            cont++;
        }
        fread(&doc, sizeof(struct documento),1, fdoc);
    }
    while(!feof(fdoc));
    printf("\n#Numero de Registros=%d",cont);
    getch();
}
void excluir(void)
{
    int pos;
    pos=busca();
    if(pos==-1)
    {
        printf("\nNumero inexistente no arquivo");
        getch();
    }
    else
    {
        if(pos==-2)
        {
            printf("\nNumero excluido do arquivo");
            getch();
        }
        else
        {
            abrir("rb+");
            fseek(fdoc, pos*sizeof(struct documento), SEEK_SET);
            fread(&doc, sizeof(struct documento), 1, fdoc);
            printf("\n---------------------------------------");
            printf("\nNumero: %s",doc.numero);
            printf("\nAno: %s",doc.ano);
            printf("\nTipo: %s",doc.tipo_cod);
            printf("\nResponsavel: %s",doc.resp_cod);
            printf("\nData: %s",doc.data);
            printf("\nAssunto: %s",doc.assunto);
            printf("\nInativo: %s",doc.inativo);
            printf("\nEste Registro #%d sera excluido",(pos+1));
            getch();
//strcpy(reg.status,"0");
            doc.status='0';
            fseek(fdoc, pos*sizeof(struct documento), SEEK_SET);
            if(fwrite(&doc, sizeof(struct documento), 1, fdoc)!=1)
            {
                printf("\nErro na gravacao!");
                getch();
            }
            else
            {
                printf("\nExclusao feita com sucesso!");
                getch();
            }
        }
    }
    fclose(fdoc);
}
