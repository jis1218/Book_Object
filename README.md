# ver 1

##### Theater 클래스 안에 다음과 같은 메서드가 있는데 audience 객체와 ticketSeller 객체가 Theater의 통제를 받는 수동적인 존재
##### 그리고 변경에 취약한 코드 - 세부적인 사실 중 한가지라도 바뀌면 해당 클래스뿐만 아니라 클래스에 의존하는 Theater도 함께 변경해야 함
##### 어떤 클래스가 다른 클래스의 내부에 대해 많이 알면 알수록 변경하기 힘들어짐, 최소한의 의존성만 필요
```java
public void enter(Audience audience) {
        if (audience.getBag().hasInvitation()) {
        Ticket ticket = ticketSeller.getTicketOffice().getTicket();
        audience.getBag().setTicket(ticket);
        } else {
        Ticket ticket = ticketSeller.getTicketOffice().getTicket();
        audience.getBag().minusAmount(ticket.getFee());
        ticketSeller.getTicketOffice().plusAmount(ticket.getFee());
        audience.getBag().setTicket(ticket);
        }
        }
```

# ver 2
##### 그러므로 결합도를 낮춰 변경이 용이한 설계를 해야 한다.
##### 자율성을 높여보자, 아래 코드들이 다 TicketSeller 클래스로 들어갔다.
##### 그렇게 해서 Theater 클래스에서 ticketOffice를 가져오는 일이 없어졌다.
```java
if (audience.getBag().hasInvitation()) {
        Ticket ticket = ticketSeller.getTicketOffice().getTicket();
        audience.getBag().setTicket(ticket);
        } else {
        Ticket ticket = ticketSeller.getTicketOffice().getTicket();
        audience.getBag().minusAmount(ticket.getFee());
        ticketSeller.getTicketOffice().plusAmount(ticket.getFee());
        audience.getBag().setTicket(ticket);
        }
```

##### 결국 객체 지향의 핵심은 책임을 분산시키는 것이다. 각 객체는 자신을 스스로 책임진다.