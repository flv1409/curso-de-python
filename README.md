 #Cálculo de Impostos em uma Fatura de Compras



import java.util.*;


public class ImpostosFatura {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        // Lê o número de produtos
        int n = scanner.nextInt();
        
        // Variável para armazenar o valor total da fatura
        double totalFatura = 0.0;
        
        // Loop para ler os produtos
        for (int i = 0; i < n; i++) {
            // Lê valor do produto
            double valorProduto = scanner.nextDouble();
            
            // Lê categoria do produto
            String categoria = scanner.next();
            
            double imposto = 0.0;
            
            // Calcula o imposto baseado na categoria
            if (categoria.equals("A")) {
                imposto = valorProduto * 0.10;
            } else if (categoria.equals("B")) {
                imposto = valorProduto * 0.15;
            } else if (categoria.equals("C")) {
                imposto = valorProduto * 0.20;
            }
            
            // Soma o valor do produto com o imposto ao total da fatura
            totalFatura += valorProduto + imposto;
        }
        
        // Imprime o valor total da fatura com 2 casas decimais
        System.out.printf("%.2f\n", totalFatura);
        
        scanner.close();
    }
}


#Simulação de Fila de Atendimento ao Cliente



import java.util.*;


public class FilaAtendimento {


    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        // Lê o número de clientes
        int n = scanner.nextInt();
        
        // Lista para armazenar os clientes: [id, prioridade, ordemEntrada]
        List<int[]> fila = new ArrayList<>();
        
        // Lê os clientes
        for (int i = 0; i < n; i++) {
            int id = scanner.nextInt();
            int prioridade = scanner.nextInt();
            fila.add(new int[]{id, prioridade, i}); // guarda ordem de entrada como desempate
        }
        
        // Ordena a fila pela prioridade (decrescente), e em caso de empate, pela ordem de entrada
        Collections.sort(fila, new Comparator<int[]>() {
            @Override
            public int compare(int[] c1, int[] c2) {
                if (c1[1] != c2[1]) {
                    return Integer.compare(c2[1], c1[1]); // prioridade decrescente
                } else {
                    return Integer.compare(c1[2], c2[2]); // ordem de chegada
                }
            }
        });
        
        // Imprime os IDs dos clientes na ordem de atendimento
        for (int i = 0; i < fila.size(); i++) {
            System.out.print(fila.get(i)[0]);
            if (i < fila.size() - 1) {
                System.out.print(" ");
            }
        }
        
        scanner.close();
    }
}


 #Ordenação de Vendas de Produtos em uma Loja Online



import java.util.*;


public class VendasProdutos {


     public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        int n = scanner.nextInt();
        scanner.nextLine();  
        
        List<String[]> produtos = new ArrayList<>();
        
        // Lê os produtos com a quantidade vendida e o preço
        for (int i = 0; i < n; i++) {
            String linha = scanner.nextLine();
            String[] partes = linha.split(" ");
            
            String nome = partes[0];
            int quantidade = Integer.parseInt(partes[1]);
            double preco = Double.parseDouble(partes[2]);
            
            produtos.add(new String[]{nome, String.valueOf(quantidade), String.valueOf(preco)});
        }
        
        // Ordena os produtos:
        // 1) Quantidade vendida (decrescente)
        // 2) Em caso de empate, preço (decrescente)
        produtos.sort((a, b) -> {
            int q1 = Integer.parseInt(a[1]);
            int q2 = Integer.parseInt(b[1]);
            double p1 = Double.parseDouble(a[2]);
            double p2 = Double.parseDouble(b[2]);
            
            if (q1 != q2) {
                return Integer.compare(q2, q1); // quantidade desc
            } else {
                return Double.compare(p2, p1); // preço desc
            }
        });
        
        // Imprime os produtos na ordem correta
        for (int i = 0; i < produtos.size(); i++) {
            System.out.print(produtos.get(i)[0]);
            if (i < produtos.size() - 1) {
                System.out.print(" ");
            }
        }
        
        scanner.close();
    }
}
