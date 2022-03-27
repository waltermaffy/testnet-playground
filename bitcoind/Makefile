BITCOIND=bitcoind
BITCOINGUI=bitcoin-qt
BITCOINCLI=bitcoin-cli
B1_FLAGS=
B2_FLAGS=
B1=-datadir=1 $(B1_FLAGS)
B2=-datadir=2 $(B2_FLAGS)
BLOCKS=1
ADDRESS=
AMOUNT=
ACCOUNT=

start:
	$(BITCOIND) $(B1) -daemon -fallbackfee=0.0002
	$(BITCOIND) $(B2) -daemon -fallbackfee=0.0002

start-gui:
	$(BITCOINGUI) $(B1) &
	$(BITCOINGUI) $(B2) &

generate:
	$(BITCOINCLI) $(B1) -generate $(BLOCKS)

createwallet:
	$(BITCOINCLI) $(B1) createwallet wallet1
	$(BITCOINCLI) $(B2) createwallet wallet2

getinfo:
	$(BITCOINCLI) $(B1) -getinfo
	$(BITCOINCLI) $(B2) -getinfo

sendfrom1:
	$(BITCOINCLI) $(B1) sendtoaddress $(ADDRESS) $(AMOUNT) -fallbackfee=0.0001

sendfrom2:
	$(BITCOINCLI) $(B2) sendtoaddress $(ADDRESS) $(AMOUNT)

address1:
	$(BITCOINCLI) $(B1) getnewaddress $(ACCOUNT)

address2:
	$(BITCOINCLI) $(B2) getnewaddress $(ACCOUNT)

stop:
	$(BITCOINCLI) $(B1) stop
	$(BITCOINCLI) $(B2) stop

clean:
	find 1/regtest/* -not -name 'server.*' -delete
	find 2/regtest/* -not -name 'server.*' -delete

docker-build:
	docker build -t bitcoin-test .

docker-run:
	docker run -t -i -p 19001:19001 -p 19011:19011 -v $(PWD):/home/tester/bitcoin-testnet-box bitcoin-test