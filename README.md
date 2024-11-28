package pjfinaltxt;

import java.io.*;
import java.util.ArrayList;
import java.util.List;

public class Aluno {

    // Cadastrar aluno
    public static void cadastrarAluno(String nome, int idade, String matricula) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter("alunos.txt", true))) {
            writer.write(nome + "," + idade + "," + matricula);
            writer.newLine();
            System.out.println("Aluno cadastrado com sucesso!");
        } catch (IOException e) {
            System.out.println("Erro ao gravar no arquivo: " + e.getMessage());
        }
    }

    // Consultar aluno
    public static void consultarAluno(String matricula) {
        try (BufferedReader reader = new BufferedReader(new FileReader("alunos.txt"))) {
            String linha;
            boolean encontrado = false;
            while ((linha = reader.readLine()) != null) {
                String[] dados = linha.split(",");
                if (dados[2].equals(matricula)) {
                    System.out.println("Aluno encontrado: " + linha);
                    encontrado = true;
                    break;
                }
            }
            if (!encontrado) {
                System.out.println("Aluno não encontrado.");
            }
        } catch (IOException e) {
            System.out.println("Erro ao ler o arquivo: " + e.getMessage());
        }
    }

    // Editar aluno
    public static void editarAluno(String matricula, String novoNome, int novaIdade) {
        try {
            List<String> alunos = new ArrayList<>();
            BufferedReader reader = new BufferedReader(new FileReader("alunos.txt"));
            String linha;
            boolean alunoEditado = false;

            while ((linha = reader.readLine()) != null) {
                String[] dados = linha.split(",");
                if (dados[2].equals(matricula)) {
                    alunos.add(novoNome + "," + novaIdade + "," + matricula);
                    alunoEditado = true;
                } else {
                    alunos.add(linha);
                }
            }
            reader.close();

            if (alunoEditado) {
                BufferedWriter writer = new BufferedWriter(new FileWriter("alunos.txt"));
                for (String aluno : alunos) {
                    writer.write(aluno);
                    writer.newLine();
                }
                writer.close();
                System.out.println("Aluno editado com sucesso!");
            } else {
                System.out.println("Aluno não encontrado para edição.");
            }

        } catch (IOException e) {
            System.out.println("Erro ao editar aluno: " + e.getMessage());
        }
    }

    // Excluir aluno
    public static void excluirAluno(String matricula) {
        try {
            List<String> alunos = new ArrayList<>();
            BufferedReader reader = new BufferedReader(new FileReader("alunos.txt"));
            String linha;
            boolean alunoExcluido = false;

            while ((linha = reader.readLine()) != null) {
                String[] dados = linha.split(",");
                if (dados[2].equals(matricula)) {
                    alunoExcluido = true;
                } else {
                    alunos.add(linha);
                }
            }
            reader.close();

            if (alunoExcluido) {
                BufferedWriter writer = new BufferedWriter(new FileWriter("alunos.txt"));
                for (String aluno : alunos) {
                    writer.write(aluno);
                    writer.newLine();
                }
                writer.close();
                System.out.println("Aluno excluído com sucesso!");
            } else {
                System.out.println("Aluno não encontrado para exclusão.");
            }

        } catch (IOException e) {
            System.out.println("Erro ao excluir aluno: " + e.getMessage());
        }
    }
}
package pjfinaltxt;

import java.io.*;

public class Professor {

    // Cadastrar professor
    public static void cadastrarProfessor(String nome, String especialidade) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter("professores.txt", true))) {
            writer.write(nome + "," + especialidade);
            writer.newLine();
            System.out.println("Professor cadastrado com sucesso!");
        } catch (IOException e) {
            System.out.println("Erro ao gravar no arquivo: " + e.getMessage());
        }
    }

    // Consultar professor
    public static void consultarProfessor(String nome) {
        try (BufferedReader reader = new BufferedReader(new FileReader("professores.txt"))) {
            String linha;
            boolean encontrado = false;
            while ((linha = reader.readLine()) != null) {
                String[] dados = linha.split(",");
                if (dados[0].equalsIgnoreCase(nome)) {
                    System.out.println("Professor encontrado: " + linha);
                    encontrado = true;
                    break;
                }
            }
            if (!encontrado) {
                System.out.println("Professor não encontrado.");
            }
        } catch (IOException e) {
            System.out.println("Erro ao ler o arquivo: " + e.getMessage());
        }
    }

    // Editar professor
    public static void editarProfessor(String nome, String novaEspecialidade) {
        try {
            File inputFile = new File("professores.txt");
            File tempFile = new File("temp_professores.txt");

            BufferedReader reader = new BufferedReader(new FileReader(inputFile));
            BufferedWriter writer = new BufferedWriter(new FileWriter(tempFile));

            String linha;
            boolean encontrado = false;
            while ((linha = reader.readLine()) != null) {
                String[] dados = linha.split(",");
                if (dados[0].equalsIgnoreCase(nome)) {
                    writer.write(nome + "," + novaEspecialidade);
                    writer.newLine();
                    encontrado = true;
                } else {
                    writer.write(linha);
                    writer.newLine();
                }
            }
            reader.close();
            writer.close();
            if (encontrado) {
                inputFile.delete();
                tempFile.renameTo(inputFile);
                System.out.println("Professor editado com sucesso!");
            } else {
                System.out.println("Professor não encontrado.");
            }
        } catch (IOException e) {
            System.out.println("Erro ao editar professor: " + e.getMessage());
        }
    }

    // Excluir professor
    public static void excluirProfessor(String nome) {
        try {
            File inputFile = new File("professores.txt");
            File tempFile = new File("temp_professores.txt");

            BufferedReader reader = new BufferedReader(new FileReader(inputFile));
            BufferedWriter writer = new BufferedWriter(new FileWriter(tempFile));

            String linha;
            boolean encontrado = false;
            while ((linha = reader.readLine()) != null) {
                String[] dados = linha.split(",");
                if (dados[0].equalsIgnoreCase(nome)) {
                    encontrado = true;
                    continue;
                }
                writer.write(linha);
                writer.newLine();
            }
            reader.close();
            writer.close();
            if (encontrado) {
                inputFile.delete();
                tempFile.renameTo(inputFile);
                System.out.println("Professor excluído com sucesso!");
            } else {
                System.out.println("Professor não encontrado.");
            }
        } catch (IOException e) {
            System.out.println("Erro ao excluir professor: " + e.getMessage());
        }
    }
}
package pjfinaltxt;

import java.io.*;

public class Curso {

    // Cadastrar curso
    public static void cadastrarCurso(String nome, int cargaHoraria) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter("cursos.txt", true))) {
            writer.write(nome + "," + cargaHoraria);
            writer.newLine();
            System.out.println("Curso cadastrado com sucesso!");
        } catch (IOException e) {
            System.out.println("Erro ao gravar no arquivo: " + e.getMessage());
        }
    }

    // Consultar curso
    public static void consultarCurso(String nome) {
        try (BufferedReader reader = new BufferedReader(new FileReader("cursos.txt"))) {
            String linha;
            boolean encontrado = false;
            while ((linha = reader.readLine()) != null) {
                String[] dados = linha.split(",");
                if (dados[0].equalsIgnoreCase(nome)) {
                    System.out.println("Curso encontrado: " + linha);
                    encontrado = true;
                    break;
                }
            }
            if (!encontrado) {
                System.out.println("Curso não encontrado.");
            }
        } catch (IOException e) {
            System.out.println("Erro ao ler o arquivo: " + e.getMessage());
        }
    }

    // Editar curso
    public static void editarCurso(String nome, int novaCargaHoraria) {
        try {
            File inputFile = new File("cursos.txt");
            File tempFile = new File("temp_cursos.txt");

            BufferedReader reader = new BufferedReader(new FileReader(inputFile));
            BufferedWriter writer = new BufferedWriter(new FileWriter(tempFile));

            String linha;
            boolean encontrado = false;
            while ((linha = reader.readLine()) != null) {
                String[] dados = linha.split(",");
                if (dados[0].equalsIgnoreCase(nome)) {
                    writer.write(nome + "," + novaCargaHoraria);
                    writer.newLine();
                    encontrado = true;
                } else {
                    writer.write(linha);
                    writer.newLine();
                }
            }
            reader.close();
            writer.close();
            if (encontrado) {
                inputFile.delete();
                tempFile.renameTo(inputFile);
                System.out.println("Curso editado com sucesso!");
            } else {
                System.out.println("Curso não encontrado.");
            }
        } catch (IOException e) {
            System.out.println("Erro ao editar curso: " + e.getMessage());
        }
    }

    // Excluir curso
    public static void excluirCurso(String nome) {
        try {
            File inputFile = new File("cursos.txt");
            File tempFile = new File("temp_cursos.txt");

            BufferedReader reader = new BufferedReader(new FileReader(inputFile));
            BufferedWriter writer = new BufferedWriter(new FileWriter(tempFile));

            String linha;
            boolean encontrado = false;
            while ((linha = reader.readLine()) != null) {
                String[] dados = linha.split(",");
                if (dados[0].equalsIgnoreCase(nome)) {
                    encontrado = true;
                    continue;
                }
                writer.write(linha);
                writer.newLine();
            }
            reader.close();
            writer.close();
            if (encontrado) {
                inputFile.delete();
                tempFile.renameTo(inputFile);
                System.out.println("Curso excluído com sucesso!");
            } else {
                System.out.println("Curso não encontrado.");
            }
        } catch (IOException e) {
            System.out.println("Erro ao excluir curso: " + e.getMessage());
        }
    }
}
package pjfinaltxt;

import java.io.*;

public class Relatorios {

    // Relatório de Alunos
	public static void gerarRelatorioAlunos() {
        try (BufferedReader reader = new BufferedReader(new FileReader("alunos.txt"))) {
            String linha;
            System.out.println("Relatório de Alunos:");
            System.out.println("Nome | Idade | Matrícula | Cursos");
            while ((linha = reader.readLine()) != null) {
                String[] dados = linha.split(",");
                if (dados.length >= 3) { // Verifica se há pelo menos 3 elementos no array
                    String nomeAluno = dados[0].trim();
                    String idade = dados[1].trim();
                    String matricula = dados[2].trim();
                    String cursosVinculados = buscarCursosVinculadosAluno(matricula);  // Busca os cursos do aluno
                    System.out.println(nomeAluno + " | " + idade + " | " + matricula + " | " + cursosVinculados);
                } else {
                    System.out.println("Linha inválida: " + linha);
                }
            }
        } catch (IOException e) {
            System.out.println("Erro ao gerar relatório de alunos: " + e.getMessage());
        }
    }

    // Relatório de Professores
    public static void gerarRelatorioProfessores() {
        try (BufferedReader reader = new BufferedReader(new FileReader("professores.txt"))) {
            String linha;
            System.out.println("Relatório de Professores:");
            System.out.println("Nome | Especialidade | Cursos");
            while ((linha = reader.readLine()) != null) {
                String[] dados = linha.split(",");
                if (dados.length >= 2) {
                    String nomeProfessor = dados[0].trim();
                    String especialidade = dados[1].trim();
                    String cursosVinculados = buscarCursosVinculadosProfessor(nomeProfessor); // Busca os cursos do professor
                    System.out.println(nomeProfessor + " | " + especialidade + " | " + cursosVinculados);
                }
            }
        } catch (IOException e) {
            System.out.println("Erro ao gerar relatório de professores: " + e.getMessage());
        }
    }

    // Método para buscar cursos vinculados a um aluno
    public static String buscarCursosVinculadosAluno(String matriculaAluno) {
        StringBuilder cursosVinculados = new StringBuilder();
        try (BufferedReader reader = new BufferedReader(new FileReader("alunos_cursos.txt"))) {
            String linha;
            while ((linha = reader.readLine()) != null) {
                if (linha.contains(matriculaAluno)) {
                    // A linha deve ter o formato "Aluno: <matricula> vinculado ao curso: <nomeCurso>"
                    String[] dados = linha.split("vinculado ao curso: ");
                    if (dados.length > 1) {
                        String nomeCurso = dados[1].trim();
                        cursosVinculados.append(nomeCurso).append(" ");
                    }
                }
            }
        } catch (IOException e) {
            System.out.println("Erro ao buscar cursos vinculados ao aluno: " + e.getMessage());
        }
        return cursosVinculados.length() > 0 ? cursosVinculados.toString() : "Nenhum curso vinculado";
    }

    // Método para buscar cursos vinculados a um professor
    public static String buscarCursosVinculadosProfessor(String nomeProfessor) {
        StringBuilder cursosVinculados = new StringBuilder();
        try (BufferedReader reader = new BufferedReader(new FileReader("professores_cursos.txt"))) {
            String linha;
            while ((linha = reader.readLine()) != null) {
                if (linha.contains(nomeProfessor)) {
                    // A linha deve ter o formato "Professor: <nomeProfessor> vinculado ao curso: <nomeCurso>"
                    String[] dados = linha.split("vinculado ao curso: ");
                    if (dados.length > 1) {
                        String nomeCurso = dados[1].trim();
                        cursosVinculados.append(nomeCurso).append(" ");
                    }
                }
            }
        } catch (IOException e) {
            System.out.println("Erro ao buscar cursos vinculados ao professor: " + e.getMessage());
        }
        return cursosVinculados.length() > 0 ? cursosVinculados.toString() : "Nenhum curso vinculado";
    }

    public static void main(String[] args) {
        gerarRelatorioAlunos();
        gerarRelatorioProfessores();
    }

    // Método para gerar relatório de cursos, alunos e professores vinculados
    public static void gerarRelatorioCursos() {
        try (BufferedReader reader = new BufferedReader(new FileReader("cursos.txt"))) {
            String linha;
            while ((linha = reader.readLine()) != null) {
                String[] dadosCurso = linha.split(",");
                String nomeCurso = dadosCurso[0];
                System.out.println("Curso: " + nomeCurso);
                System.out.println("Carga Horária: " + dadosCurso[1]);

                // Buscar alunos e professores vinculados ao curso
                String alunos = buscarCursosVinculadosAluno(nomeCurso);
                String professores = buscarCursosVinculadosProfessor(nomeCurso);

                System.out.println("Alunos: " + alunos);
                System.out.println("Professores: " + professores);
                System.out.println("-------------------------------");
            }
        } catch (IOException e) {
            System.out.println("Erro ao gerar relatório de cursos: " + e.getMessage());
        }
    }
}
package pjfinaltxt;

import java.io.*;

public class Vincular {

    // Vincular aluno ao curso
	public static void vincularAluno(String matricula, String nomeCurso) {
        try {
            boolean alunoExiste = false;
            try (BufferedReader reader = new BufferedReader(new FileReader("alunos.txt"))) {
                String linha;
                while ((linha = reader.readLine()) != null) {
                    String[] dados = linha.split(",");
                    if (dados.length >= 3 && dados[2].trim().equals(matricula)) { // Garante que a linha tenha ao menos 3 elementos
                        alunoExiste = true;
                        break;
                    }
                }
            }

            boolean cursoExiste = false;
            try (BufferedReader reader = new BufferedReader(new FileReader("cursos.txt"))) {
                String linha;
                while ((linha = reader.readLine()) != null) {
                    String[] dados = linha.split(",");
                    if (dados.length >= 1 && dados[0].trim().equalsIgnoreCase(nomeCurso)) { // Garante que a linha tenha pelo menos 1 elemento
                        cursoExiste = true;
                        break;
                    }
                }
            }

            if (alunoExiste && cursoExiste) {
                try (BufferedWriter writer = new BufferedWriter(new FileWriter("alunos_cursos.txt", true))) {
                    writer.write("Aluno: " + matricula + " vinculado ao curso: " + nomeCurso);
                    writer.newLine();
                    System.out.println("Aluno vinculado ao curso com sucesso!");
                }
            } else {
                if (!alunoExiste) {
                    System.out.println("Aluno não encontrado.");
                }
                if (!cursoExiste) {
                    System.out.println("Curso não encontrado.");
                }
            }
} catch (IOException e) {
            System.out.println("Erro ao vincular aluno ao curso: " + e.getMessage());
        }
    }

    public static void main(String[] args) {
        // Testando o método vincularAluno
        vincularAluno("12345", "Matemática");
    }


    // Vincular professor ao curso
    public static void vincularProfessor(String nomeProfessor, String nomeCurso) {
        try {
            boolean professorExiste = false;
            try (BufferedReader reader = new BufferedReader(new FileReader("professores.txt"))) {
                String linha;
                while ((linha = reader.readLine()) != null) {
                    String[] dados = linha.split(",");
                    if (dados[0].equalsIgnoreCase(nomeProfessor)) {
                        professorExiste = true;
                        break;
                    }
                }
            }

            boolean cursoExiste = false;
            try (BufferedReader reader = new BufferedReader(new FileReader("cursos.txt"))) {
                String linha;
                while ((linha = reader.readLine()) != null) {
                    String[] dados = linha.split(",");
                    if (dados[0].equalsIgnoreCase(nomeCurso)) {
                        cursoExiste = true;
                        break;
                    }
                }
            }

            if (professorExiste && cursoExiste) {
                try (BufferedWriter writer = new BufferedWriter(new FileWriter("professores_cursos.txt", true))) {
                    writer.write("Professor: " + nomeProfessor + " vinculado ao curso: " + nomeCurso);
                    writer.newLine();
                    System.out.println("Professor vinculado ao curso com sucesso!");
                }
            } else {
                if (!professorExiste) {
                    System.out.println("Professor não encontrado.");
                }
                if (!cursoExiste) {
                    System.out.println("Curso não encontrado.");
                }
            }

        } catch (IOException e) {
            System.out.println("Erro ao vincular professor ao curso: " + e.getMessage());
        }
    }
}
package pjfinaltxt;

import java.util.Scanner;

public class main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        while (true) {
            System.out.println("1. Cadastrar Aluno");
            System.out.println("2. Consultar Aluno");
            System.out.println("3. Editar Aluno");
            System.out.println("4. Excluir Aluno");
            System.out.println("5. Cadastrar Professor");
            System.out.println("6. Consultar Professor");
            System.out.println("7. Editar Professor");
            System.out.println("8. Excluir Professor");
            System.out.println("9. Cadastrar Curso");
            System.out.println("10. Consultar Curso");
            System.out.println("11. Editar Curso");
            System.out.println("12. Excluir Curso");
            System.out.println("13. Vincular Aluno ao Curso");
            System.out.println("14. Vincular Professor ao Curso");
            System.out.println("15. Gerar Relatório de Alunos");
            System.out.println("16. Gerar Relatório de Professores");
            System.out.println("17. Gerar Relatório de Cursos");
            System.out.println("18. Sair");

            int opcao = sc.nextInt();
            sc.nextLine(); // Limpar buffer

            switch (opcao) {
                case 1:
                    System.out.print("Nome do Aluno: ");
                    String nomeAluno = sc.nextLine();
                    System.out.print("Idade do Aluno: ");
                    int idadeAluno = sc.nextInt();
                    sc.nextLine(); // Limpar buffer
                    System.out.print("Matrícula do Aluno: ");
                    String matriculaAluno = sc.nextLine();
                    Aluno.cadastrarAluno(nomeAluno, idadeAluno, matriculaAluno);
                    break;
                case 2:
                    System.out.print("Matrícula do Aluno: ");
                    String matriculaConsulta = sc.nextLine();
                    Aluno.consultarAluno(matriculaConsulta);
                    break;
                case 3:
                    System.out.print("Matrícula do Aluno: ");
                    String matriculaEditar = sc.nextLine();
                    System.out.print("Novo Nome do Aluno: ");
                    String novoNomeAluno = sc.nextLine();
                    System.out.print("Nova Idade do Aluno: ");
                    int novaIdadeAluno = sc.nextInt();
                    sc.nextLine(); // Limpar buffer
                    Aluno.editarAluno(matriculaEditar, novoNomeAluno, novaIdadeAluno);
                    break;
                case 4:
                    System.out.print("Matrícula do Aluno: ");
                    String matriculaExcluir = sc.nextLine();
                    Aluno.excluirAluno(matriculaExcluir);
                    break;
                case 5:
                    System.out.print("Nome do Professor: ");
                    String nomeProfessor = sc.nextLine();
                    System.out.print("Especialidade do Professor: ");
                    String especialidadeProfessor = sc.nextLine();
                    Professor.cadastrarProfessor(nomeProfessor, especialidadeProfessor);
                    break;
                case 6:
                    System.out.print("Nome do Professor: ");
                    String professorConsulta = sc.nextLine();
                    Professor.consultarProfessor(professorConsulta);
                    break;
                case 7:
                    System.out.print("Nome do Professor: ");
                    String nomeProfessorEditar = sc.nextLine();
                    System.out.print("Nova Especialidade: ");
                    String novaEspecialidade = sc.nextLine();
                    Professor.editarProfessor(nomeProfessorEditar, novaEspecialidade);
                    break;
                case 8:
                    System.out.print("Nome do Professor: ");
                    String nomeProfessorExcluir = sc.nextLine();
                    Professor.excluirProfessor(nomeProfessorExcluir);
                    break;
                case 9:
                    System.out.print("Nome do Curso: ");
                    String nomeCurso = sc.nextLine();
                    System.out.print("Carga Horária do Curso: ");
                    int cargaHorariaCurso = sc.nextInt();
                    sc.nextLine(); // Limpar buffer
                    Curso.cadastrarCurso(nomeCurso, cargaHorariaCurso);
                    break;
                case 10:
                    System.out.print("Nome do Curso: ");
                    String nomeCursoConsulta = sc.nextLine();
                    Curso.consultarCurso(nomeCursoConsulta);
                    break;
                case 11:
                    System.out.print("Nome do Curso: ");
                    String nomeCursoEditar = sc.nextLine();
                    System.out.print("Nova Carga Horária: ");
                    int novaCargaHoraria = sc.nextInt();
                    sc.nextLine(); // Limpar buffer
                    Curso.editarCurso(nomeCursoEditar, novaCargaHoraria);
                    break;
                case 12:
                    System.out.print("Nome do Curso: ");
                    String nomeCursoExcluir = sc.nextLine();
                    Curso.excluirCurso(nomeCursoExcluir);
                    break;
                case 13:
                    System.out.print("Matrícula do Aluno: ");
                    String matriculaVinculo = sc.nextLine();
                    System.out.print("Nome do Curso: ");
                    String cursoVinculo = sc.nextLine();
                    Vincular.vincularAluno(matriculaVinculo, cursoVinculo);
                    break;
                case 14:
                    System.out.print("Nome do Professor: ");
                    String professorVinculo = sc.nextLine();
                    System.out.print("Nome do Curso: ");
                    String cursoVinculoProfessor = sc.nextLine();
                    Vincular.vincularProfessor(professorVinculo, cursoVinculoProfessor);
                    break;
                case 15:
                    Relatorios.gerarRelatorioAlunos();
                    break;
                case 16:
                    Relatorios.gerarRelatorioProfessores();
                    break;
                case 17:
                    Relatorios.gerarRelatorioCursos();
                    break;
                case 18:
                    System.out.println("Saindo...");
                    sc.close();
                    return;
                default:
                    System.out.println("Opção inválida.");
            }
        }
    }
}
