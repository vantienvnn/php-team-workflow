PHP UNIT TEST EXAMPLE
=====================

Example 1: Use mock for test send email function

- In this test we want to check the function sendBookingEmail working or not
- Class EmailRepository
```php
class EmailRepository
{

    protected $client;

    public function setClient($client)
    {
        $this->client = $client;
    }

    public function getClient()
    {
        if (empty($this->client)) {
            $this->client = new EmailSender();
        }
        return $this->client;
    }

    public function sendBookingEmail($email)
    {
        $emailModel = new EmailModel(array('email' => $email));
        $emailModel->save();
        return $this->client->send('Any Value', $email);
    }

}
```
- Example Test file
```
class EmailRepositoryTest extends TestCase
{

    function testSendBookingEmailOk()
    {
        $emailResult = '{status:ok}';
        $emailSenderMock = Mockery::mock();
        $emailSenderMock->shouldReceive('send')
            ->with(Mockery::any(), 'tien@simble.io')
            ->once()
            ->andReturn($emailResult);
        
        $emailRepository = app(\App\Repositories\EmailRepository::class);
        $emailRepository->setClient($emailSenderMock);
        $result = $emailRepository->sendBookingEmail('tien@simble.io');
        $this->assertEquals($result, $emailResult);
    }

}
```
