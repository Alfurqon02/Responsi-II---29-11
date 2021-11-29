# Responsi-II---29-11
29-November-2021
Playlist With Queue

              /* RESPONSI II Konsep Pemrogaman - Playlist Lagu Menggunakan Queue
                  Mohammad Al Furqon
                  M0521044
                  Informatika B
                  Universitas Sebelas Maret
              */
              /*
                  Di Program Ini Kita Bisa Membuat Playlist Baru
                  Bisa Menyimpan Lagu Ke Playlist Yang Sudah Ada
                  Bisa Menyimpan Lagu Ke Playlist Baru
                  Bisa Menambah Lagu Ke Playlist
                  Bisa Memutar Lagu Yang Ada Di Playlist
              */
              /*
              Program Ini Dibuat Untuk Memenuhi Responsi II Mata Kuliah Konsep Pemrogaman
              Mohon Maaf Jika Terdapat Kesalahan/Bug Dalam Program
              */

              #include <stdio.h>
              #include <stdlib.h>
              #include <string.h>
              #include <windows.h>

              struct myPlaylist{
                  char judullagu[50];

                  struct myPlaylist *next;
              }; typedef struct myPlaylist mpl; typedef mpl *mplPtr;

              mplPtr start = NULL;
              mplPtr end = NULL;

              //=====LIST FUNGSI YANG DIGUNAKAN=====

              //Fungsi Untuk Membuat Playlist Baru
              void buatplaylist();
              //Fungsi Menambah Lagu Ke Playlist (Enqueue)
              void tambahLagu(char judullagu[]);
              //Fungsi Untuk Mengambil Playlist Dari File Yang Berisi Kumpulan Lagu
              void importPlaylist();
              //Fungsi Enqueue
              void enqueue();
              //Fungsi Dequeue
              void dequeue();
              //Fungsi Untuk Menyimpan Lagu Ke Playlist Yang Sudah Ada
              void saveToPlaylist();
              //Fungsi Untuk Menyimpan Lagu Ke Playlist Baru
              void savePlaylist();
              //Fungsi Untuk Menampilkan Pilihan Menu
              void menu();

              //Fungsi main();
              int main(){
                  menu();
              }

              void buatPlaylist(){
                  struct myPlaylist q;

                  FILE *f;
                  int i, n;
                  char fname[50];
                  char src[10] = ".txt";
                  char playlist[50];
                  printf ("Masukkan Nama Playlist : ");
                  scanf ("%s", fname);
                  strcpy (playlist, fname);
                  strcat(fname, src);

                  f=fopen(fname, "w");

                   if (!f) {
                      printf ("EROR : !\n");
                      exit(EXIT_FAILURE);
                  }
                      printf ("Jumlah Lagu Yang Ingin Dimasukkan Ke Dalam Playlist : ");
                      scanf ("%d", &n);
                      for (i=0;i<n;i++)
                      {
                          printf ("Masukkan Judul Lagu : ");
                          scanf ("%s", q.judullagu);
                          fprintf(f, "%s\n", q.judullagu);
                      }
                  fclose(f);
                  printf("Playlist %s Telah Berhasil Dibuat", playlist);
              }

              void tambahLagu(char judullagu[])
              {   
                  mplPtr new = (mplPtr) malloc(sizeof(mpl));
                  strcpy(new->judullagu, judullagu);
                  new->next = NULL;

                  if(start == NULL)
                  {
                      start = new;
                      end = new;
                  } else
                  {
                      end->next = new;
                      end = new;
                  }
              }

              void importPlaylist()
              {

                  FILE *f;
                  int i, n;
                  char fname[50];
                  char src[10] = ".txt";
                  char playlist[50];
                  printf ("Masukkan Nama Playlist : ");
                  scanf ("%s", fname);
                  strcpy (playlist, fname);
                  strcat(fname, src);
                  mpl temp;
                  f=fopen(fname, "r");

                  if(f != NULL)
                  {
                      while(!feof(f))
                      {
                          fscanf(f, "%s", temp.judullagu);
                          if(!feof(f))
                          {
                              tambahLagu(temp.judullagu);
                          } else
                          {
                              break;
                          }
                      }
                  }
                  fclose(f);
                  f = NULL;
              }

              void enqueue()
              {
                  char judul[50];

                  printf("Masukkan judul lagu : ");
                  scanf("%s", judul);

                  tambahLagu(judul);
                  saveToPlaylist();
                  printf("\nLagu [%s] telah berhasil ditambahkan.\n", judul);
              }

              void dequeue()
              {   FILE *f;
                  /* if (!f) {
                      printf ("EROR : !\n");
                      exit(EXIT_FAILURE);
                  }*/
                  struct myPlaylist q;
                  if(start != NULL)
                  {
                      mplPtr delete = start;
                      start = start->next;
                      free(delete);
                  } else
                  {
                      printf("Playlist Kosong");
                  }

              }

              void saveToPlaylist()
              {
                  FILE *f;
                  int i, n;
                  char fname[50];
                  char src[10] = ".txt";
                  char playlist[50];
                  printf ("Masukkan Nama Playlist : ");
                  scanf ("%s", fname);
                  strcpy (playlist, fname);
                  strcat(fname, src);
                  mpl temp;
                  mplPtr current = start;

                   f=fopen(fname, "r");
                   if (!f) {
                      printf ("EROR : Playlist Tidak Ditemukan!\n");
                      exit(EXIT_FAILURE);
                  }
                  fclose(f);


                  f=fopen (fname, "a");
                  while(current != NULL)
                  {
                      strcpy(temp.judullagu, current->judullagu);
                      fprintf(f, "%s\n", temp.judullagu);
                      current = current->next;
                  }
                  fclose(f);
                  printf("Berhasil Menyimpan Lagu Ke Playlist %s", playlist);
                  f = NULL;
              }

              void savePlaylist()
              {
                  FILE *f;
                  int i, n;
                  char fname[50];
                  char src[10] = ".txt";
                  char playlist[50];
                  printf ("Masukkan Nama Playlist : ");
                  scanf ("%s", fname);
                  strcpy (playlist, fname);
                  strcat(fname, src);
                  mpl temp;
                  mplPtr current = start;

                  f=fopen (fname, "w");
                  while(current != NULL)
                  {
                      strcpy(temp.judullagu, current->judullagu);
                      fprintf(f, "%s\n", temp.judullagu);
                      current = current->next;
                  }
                  fclose(f);
                  printf("Berhasil Menyimpan Lagu Ke Playlist %s", playlist);
                  f = NULL;
              }

              void listLagu()
              {
                  mplPtr awal = start;
                  if(awal == NULL)
                  {
                      printf("Playlist Kosong\n");
                       return;
                  }
                  else
                  {
                      printf("Daftar Lagu\n");
                      for(int i = 1; awal != NULL; ++i)
                      {
                          printf("[%d] %s", i, awal->judullagu);
                          awal = awal->next;
                          if(awal != NULL)
                          {
                              printf("\n");
                          }
                      }
                      printf("\n---------------------------------------------------------------------------------\n");
                  }
              }

              /*void readPlaylist()
              {   
                  struct myPlaylist q;
                  FILE *f;
                  int i, n;
                  char fname[50];
                  char src[10] = ".txt";
                  char playlist[50];
                  printf ("Masukkan Nama Playlist : ");
                  scanf ("%s", fname);
                  strcpy (playlist, fname);
                  strcat(fname, src);
                  mpl temp;

                  f = fopen(fname, "r");
                  if (!f) {
                      printf ("EROR : File Tidak Ditemukan!\n");
                      exit(EXIT_FAILURE);
                  }
                  while (!feof(f))
                      {
                          fscanf(f, "%s", q.judullagu);
                          if(!feof(f))
                          {
                              tambahLagu(temp.judullagu);
                          } else
                          {
                              break;
                          }
                      }
                  fclose(f);
                  f = NULL;
              }
              */

              void menu(){
                  int pilihan1, pilihan2;
                  SetConsoleTextAttribute (GetStdHandle (STD_OUTPUT_HANDLE),9); 
                  puts  ("==============================================="); 
                  printf("|");
                  SetConsoleTextAttribute (GetStdHandle (STD_OUTPUT_HANDLE),4);
                  printf("        Selamat Datang di MyPlayList!        ");
                  SetConsoleTextAttribute (GetStdHandle (STD_OUTPUT_HANDLE),9); 
                  puts  ("|");
                  puts  ("==============================================="); 
                  printf("|");
                  SetConsoleTextAttribute (GetStdHandle (STD_OUTPUT_HANDLE),7);
                  printf(" 1. Buat PlayList                            ");
                  SetConsoleTextAttribute (GetStdHandle (STD_OUTPUT_HANDLE),9); 
                  puts("|");
                  printf("|");
                  SetConsoleTextAttribute (GetStdHandle (STD_OUTPUT_HANDLE),7);
                  printf(" 2. Lihat PlayList                           ");
                  SetConsoleTextAttribute (GetStdHandle (STD_OUTPUT_HANDLE),9); 
                  puts("|");
                  puts  ("==============================================="); 
                  SetConsoleTextAttribute (GetStdHandle (STD_OUTPUT_HANDLE),7);
                  printf ("Pilihan : ");
                  scanf ("%i", &pilihan1);
                  system ("cls");
                  if (pilihan1 == 1){
                      buatPlaylist();
                  }
                  else if (pilihan1 == 2){
                  system("cls");
                  pilihan2 :
                  importPlaylist();
                  listLagu();
                  while (pilihan2 = 1 || 2 || 3)
                  {
                  SetConsoleTextAttribute (GetStdHandle (STD_OUTPUT_HANDLE),9); 
                  puts  ("\n==============================================="); 
                  printf("|");
                  SetConsoleTextAttribute (GetStdHandle (STD_OUTPUT_HANDLE),7);
                  printf(" 1. Tambah Lagu ke PlayList                  ");
                  SetConsoleTextAttribute (GetStdHandle (STD_OUTPUT_HANDLE),9); 
                  puts("|");
                  printf("|");
                  SetConsoleTextAttribute (GetStdHandle (STD_OUTPUT_HANDLE),7);
                  printf(" 2. Putar PlayList                           ");
                  SetConsoleTextAttribute (GetStdHandle (STD_OUTPUT_HANDLE),9); 
                  puts("|");
                  printf("|");
                  SetConsoleTextAttribute (GetStdHandle (STD_OUTPUT_HANDLE),7);
                  printf(" 3. Simpan PlayList                          ");
                  SetConsoleTextAttribute (GetStdHandle (STD_OUTPUT_HANDLE),9); 
                  puts("|");
                  puts  ("==============================================="); 
                  SetConsoleTextAttribute (GetStdHandle (STD_OUTPUT_HANDLE),7);
                  printf("Pilihan : ");
                  scanf ("%i", &pilihan2);
                  switch (pilihan2)
                  {
                  case 1 :
                      enqueue();
                      break;

                  case 2 :
                      listLagu();
                      dequeue();
                      printf("Sedang Memutar Lagu");
                      break;

                  case 3 :
                      listLagu();
                      savePlaylist();
                      break;

                  default:
                      goto pilihan2;
                      break;
                  }
                  }
              }
              }
